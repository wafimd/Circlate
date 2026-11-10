# Circlate — Explained Like You're 12

Circlate is software that helps companies manage their employees. Instead of explaining all the pieces first, let's just follow what actually happens — from the moment a company signs up to the moment someone gets paid. We'll go deep on each story, because the interesting parts are in the details.

---

## Story 1 — A Company Signs Up

Imagine a company called **Nasi Lemak Co.** They have 30 employees and currently track everything in WhatsApp groups and Excel spreadsheets. The HR Admin, **Liyana**, signs up for Circlate.

The moment she submits the form, something interesting happens behind the scenes — not just one thing, but a whole sequence of steps that have to happen in a specific order. Circlate calls this a **provisioning saga**. Think of it like a checklist that the system works through automatically:

1. Create a private database space just for Nasi Lemak Co. — think of it like handing them their own section of a filing cabinet. Other companies using Circlate have their own sections. They share the same cabinet (the same servers) but they cannot reach into each other's sections at all. Circlate calls this **multi-tenancy**, and technically it works by giving each company their own named **schema** inside the database — like labelling different drawers "NasiLemakCo," "BurgerShack," and so on.

2. Create a login account for Liyana. Circlate uses a system called **Keycloak** to handle logins — think of Keycloak as the security guard at the front door. The guard knows every employee's face (username and password) and checks their ID before letting them in. Each company gets their own security guard (their own Keycloak "realm"), so there's no risk of an employee from one company accidentally logging into another company's data.

3. Load in the **rulebook**. These are the starting rules that every Brunei company must follow by law — things like "every employee must get at least 7 days of annual leave per year if they've worked less than two years." These rules don't live in the code (which would require a software update to change). They live in the database as data — so the team can update them if Brunei's Employment Order ever changes, without deploying new software.

4. Send Liyana her welcome email: "Your account is ready."

What's clever about this sequence is that if anything goes wrong partway through — say the server trips over during step 2 — the whole thing can be retried safely. Each step checks whether it already completed before doing it again. No half-built apartments.

Liyana logs in. The app looks mostly empty — just a skeleton. But it's ready.

---

## Story 2 — A New Employee Joins

Liyana, the HR Admin, adds **Zara**, a new accountant who is joining on 1 July.

Here's the interesting part: Circlate doesn't just add Zara as a person. The first decision is not "who is Zara?" but "what chair is Zara sitting in?"

**What is a position (a "chair")?**

A position is a slot in the company's structure. "Accountant, Finance Department" is a position. So is "Finance Manager" and "CEO." Each position has four key things attached to it:

1. **A place in the hierarchy** — it knows which position it reports to, and which positions report to it.
2. **A list of things it's allowed to do** — submit expenses, approve leave, view payroll, etc.
3. **A salary band** — the pay range for anyone sitting in this chair.
4. **A department** — Finance, Operations, HR, and so on.

The chair exists independently of the person. If Zara leaves and someone else joins, that new person just sits down in the same chair and inherits everything automatically. Nobody has to rebuild the setup from scratch.

**What happens when Zara is assigned her chair?**

The moment she's assigned, Circlate calculates her **permission set** — the full list of things she's allowed to do in the app. Because she's an Accountant, she gets: submit expense claims, view her own payslips, request leave, view her own profile. She does not get: approve other people's expenses, see other employees' salaries, change company settings.

This permission set gets written into a fast memory store called **Redis**. Think of Redis like a sticky note pinned on the wall next to the front door. Every time Zara tries to do something in the app, the security layer grabs the sticky note and checks: "is this on her list?" The check takes a fraction of a millisecond. If the system stored permissions only in the main database, every click would need a slow database lookup. Redis keeps it fast.

The sticky note isn't permanent — it expires after a few hours. When it expires, the app rebuilds it from the latest position assignment. This means that if Zara gets promoted and her chair changes, her permissions update automatically within hours without anyone needing to log her out and back in.

**How does Zara log in for the first time?**

Liyana sends Zara a welcome link. Zara clicks it, sets her password with the Keycloak security guard, and the guard gives her a **token** — a small piece of data that proves "I am Zara from Nasi Lemak Co." Every page she loads, she shows the security guard her token. The token contains her employee ID, which company she's from, and which position she holds — but not a list of permissions. That list lives in Redis and gets checked separately.

**The welcome notification.**

Zara receives a welcome notification in the app and by email. That notification was sent by a part of Circlate called **BC-08 Notifications** — a central post office. Every other part of Circlate deposits messages at this post office. The post office then decides: does this person want email? In-app? SMS? It checks the company's preferences and Zara's own preferences, then routes accordingly.

No other part of Circlate is allowed to send emails directly. If BC-05 Leave wants to tell someone about a leave approval, it doesn't send the email itself — it drops a note at the post office and walks away. The post office handles the rest. This keeps all notification logic in one place.

---

## Story 3 — Zara Requests Annual Leave

It's December. Zara wants to take a week off over the holidays. She opens Circlate, picks her dates (Monday 21 December to Friday 25 December), and hits submit.

Here's what happens in the next few seconds — in careful order:

**Step 1 — Counting working days.**

December 21–25 looks like 5 days. But Circlate doesn't just count calendar days. It counts **working days** — skipping weekends and public holidays. In Brunei, there are several public holidays in December. If Christmas Day falls on a Friday, Circlate won't charge Zara a leave day for it. It cross-references a table of public holidays stored in the database.

The correct answer might be 4 working days, not 5.

**Step 2 — Checking the balance.**

Zara joined on 1 July. She's entitled to 7 days per year (Brunei legal minimum for under 2 years of service). But she only worked for half a year — so her entitlement is **prorated**: 7 × (6 months ÷ 12 months) = 3.5 days, rounded up to 4.

She has 4 days available. The request costs 4 working days (after public holiday deduction). The balance check passes — just barely.

If she had tried to take 5 days, she would have seen: "You have 4 days available. This request is for 5 days." She'd need to adjust or the system would reject it.

**Step 3 — Finding the approver.**

Now the system needs to figure out who approves this. It doesn't look in a column called "Zara's manager." Instead, it climbs the **position tree**.

Zara's chair (Accountant) is linked to the Finance Manager chair above it. That link is between chairs, not between people. The system says: "Who is currently sitting in the Finance Manager chair?" The answer is **Hassan**. Hassan is the approver.

This is the whole point of the chair design. Tomorrow, if Hassan moves to a different role and **Rania** takes the Finance Manager chair, all future leave requests from Zara automatically go to Rania — without anyone updating a settings page.

**Step 4 — Writing to the outbox.**

Before the system sends Hassan any notification, it does something that might seem like extra work: it writes the pending notification into a **waiting list** in the database, called the **outbox**.

Why? Imagine the server crashes right after recording Zara's leave request but before sending Hassan's email. Without the outbox, Hassan never gets notified. Zara's leave is in the system but nobody's reviewing it. It sits in limbo forever.

With the outbox, here's the order:
1. Record Zara's leave request.
2. Write to the outbox: "Send Hassan a notification about leave request #4421."
3. These two steps happen **together in one database write** — it's all-or-nothing.
4. A background worker called the **Outbox Processor** then picks up the waiting list and sends the email.

If the server crashes after step 3, when it restarts, the Outbox Processor finds the item in the waiting list and tries again. The email might arrive a little late, but it will arrive. Nothing disappears silently.

**Step 5 — Hassan approves.**

Hassan gets the email. He clicks the approval link, adds a note ("Have a great break"), and submits. The system marks the leave request as Approved. It then writes another item to the outbox: "Tell Zara her leave was approved."

**Step 6 — Zara is notified.**

The post office picks up the outbox item, checks Zara's preferences, and sends her an in-app notification and an email. Her leave balance drops from 4 to 0 days.

**Step 7 — Payroll knows.**

At month end, the HR Admin exports the payroll report. Zara's row shows:
- Annual Leave Days: 4
- Leave Entitlement: 4 days (so the payroll processor can verify she used exactly what she was entitled to)
- Approved Expenses: —

The payroll processor takes this report to calculate Zara's December pay. The report doesn't do the salary calculation itself — that's deliberate. Circlate hands the facts to the payroll processor; the payroll processor does the maths.

---

## Story 4 — Zara Claims an Expense

Three weeks earlier, Zara took a taxi to visit a client. It cost BND 15. She opens Circlate on her phone, takes a photo of the receipt, fills in: "Client visit, Brunei Muara district, BND 15.00," and submits.

What happens:

The system stores the receipt photo and the claim details. It then needs to find an approver. The logic is similar to leave — climb the position tree — but the system is looking for the first position above Zara's that has **expense approval authority**. That authority is attached to Hassan's Finance Manager chair.

Hassan gets notified (via the post office, via the outbox — same pattern as leave). He opens the app, sees the receipt photo, checks the amount is reasonable, and clicks Approve. The claim moves to "Approved."

At month end, the payroll export shows:
- Approved Expenses: BND 15.00 (BND)

Zara receives BND 15 with her salary. No separate reimbursement process, no cheques, no chasing.

**What if Hassan thinks the amount is wrong?**

He can reject it with a note — "Please resubmit with itemised receipt." Zara gets notified. She can edit and resubmit, or withdraw the claim entirely.

**What if someone submits a fake receipt?**

The photo is stored. It's tied to Zara's employee ID. The approver saw it. If there's a dispute later, the audit trail is complete: who submitted, what photo, who approved, when. Circlate doesn't decide whether the expense is legitimate — it just makes sure there is always a human in the approval loop, and always a record.

---

## Story 5 — Hassan Goes on Holiday (and What Doesn't Break)

Hassan submits his own leave request for two weeks in January. His leave gets approved by his manager (the CEO, who sits in the chair above his).

Before Hassan leaves, the HR Admin creates an **acting assignment**: Yusof (Hassan's deputy) will temporarily sit in the Finance Manager chair from 5 January to 19 January.

This doesn't remove Hassan from his chair permanently. It layers Yusof on top of it temporarily. During this period, the system sees two people in the Finance Manager chair: Hassan (primary) and Yusof (acting). When resolving approvals, the system checks: is there an active acting assignment for this position right now? Yes — Yusof. Use Yusof.

Any leave request Zara submits between 5 and 19 January goes to Yusof automatically. Any expense claim submitted during that period goes to Yusof. All of this without Liyana having to update a single settings page.

On 20 January, Hassan comes back. The acting assignment expires. Yusof steps out of the chair. All new requests route to Hassan again.

**What if Hassan comes back early?**

Liyana can end the acting assignment early with one click. The system recalculates routing immediately. No manual cleanup needed.

**What if Yusof goes on leave too?**

The system climbs the tree further — it looks for the first position above Finance Manager with approval authority that is currently occupied and not on leave. This chain can go as high as it needs to — eventually hitting the CEO if necessary.

---

## Story 6 — A Position Goes Vacant (Recruitment)

Zara gets promoted in March. She moves from the Accountant chair to a Senior Accountant chair. The Accountant chair is now empty.

Liyana opens the **Recruitment** module. She creates a job posting for the Accountant position — the posting automatically pulls in the job title, department, and salary band from the chair definition. She doesn't need to type those in manually.

The posting goes live on the company's careers page (and optionally on job boards Circlate connects to). Candidates apply. Each application comes into the **Recruitment** module.

Here's what happens to each application:
1. The system logs it and assigns it a tracking number.
2. Liyana and Hassan can review CVs directly in Circlate.
3. When they want to invite someone to interview, they schedule it inside the app — the candidate gets a notification with the date, time, and format (video or in-person).
4. After the interview, the hiring team marks it as Pass or Fail with notes.
5. If a candidate reaches the offer stage, Circlate generates an offer letter from a template, pre-filled with the salary band and start date. Liyana reviews and sends it.
6. The candidate accepts online. Their record is now a pending employee — ready to be converted into a full employee record on their start date.

When the new employee's start date arrives, Liyana clicks "Onboard." The system creates their employee record, assigns them to the Accountant chair, generates permissions, sends the welcome email. The chair is filled again.

The whole chain — vacant chair → job posting → applicants → offer → employee — is tracked in one place, with a full audit trail of who saw which CV and what decision was made.

---

## Story 7 — The HR Admin Makes an Announcement

There's a company-wide briefing next Friday. Liyana needs to tell all 30 employees.

She opens the **Announcements** module. She types the message, sets the audience to "All Employees," and hits Publish.

What happens: Circlate sends the message to the post office (BC-08 Notifications). The post office looks at the audience filter — "all employees of Nasi Lemak Co." — and generates one notification per employee. Each notification is written to the outbox. The Outbox Processor then sends them out in batches, so the email server doesn't get hit with 30 emails at exactly the same millisecond.

Each employee sees the announcement in their in-app notification bell and in their email inbox. If they prefer only in-app notifications (they can set this in their profile), they won't get the email.

Announcements are also pinned in a feed inside the app, so an employee who was on leave when it went out can still read it when they come back.

**Can Liyana target just one department?**

Yes. She sets the audience to "Finance Department." Only Zara, Hassan, and the other Finance employees get it. Everyone else sees nothing. The audience filtering happens based on position assignments — the system checks "which employees are currently in positions that belong to the Finance department?" and sends only to them.

---

## Story 8 — Something Goes Wrong (Helpdesk)

Zara can't see her payslip for November. She opens the **Helpdesk** module and submits a ticket: "Payslip not showing — November 2025."

The ticket is routed to the HR Admin (Liyana) automatically. Liyana gets a notification. She opens the ticket, investigates, and discovers that Zara's payslip hadn't been uploaded yet — the payroll processor forgot to upload the PDF to Circlate.

Liyana uploads the missing payslip directly in the ticket, adds a note to Zara ("November payslip is now available — sorry for the delay"), and closes the ticket.

Zara gets a notification: "Your ticket has been resolved." She opens it, sees Liyana's note, and can now access the payslip.

The whole conversation is stored in the ticket. If the same issue happens again in December, there's a record: what the problem was, who fixed it, how. This is useful if Liyana is on leave and someone else is covering HR — they can read the history without calling Liyana.

---

## Story 9 — End of Year (The Books Close)

It's 31 December. The leave year ends. Nasi Lemak Co. has a policy: unused annual leave can be carried forward, but only up to 3 days. Anything above 3 days is forfeited.

At midnight, Circlate's **Year-End Job** runs automatically. It goes through every employee:

For each employee, it checks: how many unused annual leave days do they have? If it's above 3, the system writes two adjustments:
1. A carry-forward of 3 days into next year's balance.
2. A forfeiture record: "Zara forfeited 1 day on 31 Dec 2025 — policy: max 3 days carry-forward."

The forfeiture record never disappears. If Zara asks in February "why do I only have 3 days at the start of the year?" Liyana can pull up the adjustment history and show her exactly what happened and why.

On 1 January, every employee's entitlement resets to their annual allocation (based on their years of service). Zara, now in her second year, is entitled to 8 days (Brunei legal minimum for 2–5 years of service). She starts the new year with 8 + 3 carry-forward = 11 days available.

This calculation — entitlement, proration, carry-forward, forfeiture — is all stored as data records, not locked inside the code. If Nasi Lemak Co. wants to change their carry-forward policy from "3 days max" to "5 days max," Liyana changes one setting. The year-end job reads the setting and applies it. No software update needed.

---

## Story 10 — The System Has a Bad Night (What Happens When Things Break)

It's 2am on a Tuesday. Nobody is using Circlate. But the servers are still running, background jobs are ticking over, and something unexpected happens: the email provider Circlate uses goes down for 30 minutes.

During those 30 minutes, three things happen:
- An employee in a different timezone submits a leave request.
- Their manager's approval notification tries to send.
- The email provider returns an error: "Service unavailable."

Here's what Circlate does:

Because the notification was written to the **outbox** before the email was sent, the outbox item is still there with status "Failed." The Outbox Processor sees this and doesn't panic. It applies a **retry schedule**: try again in 5 minutes. If that fails, try again in 15 minutes. If that fails, try again in 30 minutes. If it still fails after several attempts, the item moves to a **dead-letter list** — a separate queue for things that couldn't be delivered after repeated tries.

At 2:35am, the email provider comes back up. The Outbox Processor picks up the failed item, retries, and succeeds. The manager gets their email — 35 minutes late, but it arrives.

If the item had ended up in the dead-letter list (say, the email address was invalid), an alert would go to the Circlate ops team: "This notification could not be delivered. Manual review required." The team can inspect the failed item, fix the problem (e.g., update the email address), and re-queue it.

The employee's leave request was recorded safely throughout. The delivery failure was an email problem, not a data problem. The underlying state was never at risk.

---

## Story 11 — Nasi Lemak Co. Grows (How the Building Scales)

Nasi Lemak Co. grows from 30 to 300 employees over two years. They're now on Circlate's mid-tier plan. They've started asking questions like: "Can our data be in its own private database instead of shared with other companies?"

This is the **Enterprise tier**. Here's what happens:

Circlate's ops team runs a migration. They:
1. Export all of Nasi Lemak Co.'s data from the shared database schema.
2. Spin up a dedicated private database for them.
3. Import the data into the private database.
4. Run a check: does every record in the new database match the original? Yes.
5. Update the system's routing: "When a request comes in from Nasi Lemak Co., connect to their private database."
6. Test that everything works.
7. Flip the switch. The app now points to the private database.

Liyana never notices. The app looks identical. Her employees see no difference. But her data is now in its own private database that no other company shares — higher isolation, higher performance for large datasets, easier for her to request a data export if she ever decides to leave Circlate.

The key insight: because every piece of Nasi Lemak Co.'s data was always tagged "this belongs to Nasi Lemak Co." (using their tenant ID), the migration was just a copy-and-redirect. The business logic didn't change at all.

---

## The Six Rules Everything Runs On

After seeing all eleven stories, the core rules become obvious:

**1. Chairs, not people.**
A position owns the rules — what it can do, who it reports to, what it can approve. A person just sits in a chair. When the person leaves, the chair stays. When someone else sits down, they inherit everything. This is why Hassan's absence doesn't break anything, why Zara's promotion doesn't require manual cleanup, and why the whole org chart stays consistent without anyone having to maintain it manually.

**2. One post office.**
Every notification — leave approved, expense rejected, announcement posted, ticket resolved — goes through BC-08 Notifications. No other part of the system is allowed to send emails directly. This means: one place to change the email templates, one place to debug delivery problems, one place to add SMS support later. Without this rule, notification logic would be scattered across a dozen different modules, each with its own bugs and its own email format.

**3. Write it down before you act.**
Every important action — notify Hassan, process this leave, send this announcement — gets written to the outbox in the same database transaction as the original change. The notification worker picks it up after. If the server crashes between the write and the send, the outbox item survives and gets retried. This is how the system guarantees that if something happened, the downstream effects will also happen — even across restarts, failures, and brief outages.

**4. Your apartment is yours.**
Every piece of data in Circlate is tagged with a tenant ID. Every database query filters by tenant ID. The system will never return data from Company A to a user from Company B — not because of access controls on the application layer, but because the data is physically separated into different database schemas. Even if a bug existed in the access control layer, the data would still be in the wrong schema to be reached.

**5. Rules are data.**
The minimum leave entitlement (7 days for under 2 years of service) is a row in a database table. The carry-forward cap is a setting. The approval routing logic is derived from position links — also in the database. When Brunei's Employment Order changes, the ops team updates a table. When Nasi Lemak Co. changes their leave policy, Liyana changes a setting. No code is deployed. No engineers are paged at 11pm.

**6. The position tree is the source of truth.**
The company's hierarchy isn't stored as a list of "who reports to whom." It's stored as a tree of chairs, each linked to the chair above it. Approvals, notifications, escalations — everything that needs to know "who is in charge here?" asks the tree. The tree is always current because the HR Admin manages chairs, not people. When someone joins, leaves, or moves, the tree updates immediately and everything downstream adjusts.

---

## What It Looks Like

Circlate is a web app with a dark sidebar on the left. The sidebar has sections: Dashboard, Employees, Attendance, Leave, Expenses, Recruitment, Documents, Reports, Organisation, Announcements, Helpdesk, Billing, Settings.

Each employee sees the same sidebar, but only the sections their position allows them to use are clickable. Zara can see the Leave section and submit a request. She can see her own expense claims. She cannot see the Payroll report — that section is visible in the sidebar but grayed out.

HR Admins see everything. They can view all employees, run the payroll export, manage positions, configure leave policies, post announcements, and respond to helpdesk tickets.

The app works on desktop and mobile browsers. The design is intentionally simple — it doesn't try to look like SAP or Workday. It tries to look like something a 30-person company could figure out without a training course.

---

## How It's Built (For Those Who Are Curious)

Under the hood, Circlate is two things: a **backend** (the engine) and a **frontend** (the dashboard).

**The backend** is written in C# (.NET). It follows a pattern called CQRS — Commands and Queries Responsibility Segregation, which is a complicated way of saying: actions that change data (like "submit a leave request") are handled separately from actions that just read data (like "show me the payroll report"). This keeps the code clean and each piece easy to test.

The backend talks to a **PostgreSQL** database — a reliable, open-source database used by companies worldwide. It also talks to **Redis** (the sticky-note memory system for permissions) and **Keycloak** (the security guard for logins).

**The frontend** is built with Next.js and React — the same technology used by some of the world's largest websites. It's what you see in the browser. It calls the backend via APIs — small messages that say things like "fetch the leave balance for employee 42" or "submit this expense claim."

**The background workers** are part of the backend. They run continuously, checking the outbox for items to process, running the year-end job at midnight on 31 December, and sending batched notifications without blocking the main app.

The whole thing runs in containers (Docker) — think of containers as standardised boxes that can run on any server without having to set up the environment from scratch. This makes it easy to move Circlate to a bigger server, or to run multiple copies for redundancy.

---

## Who Is This For?

Small and medium businesses in Brunei and Southeast Asia — the kind of company that currently runs HR on spreadsheets and WhatsApp, and needs something better without paying for a massive enterprise system.

A company with 15 employees who are tired of losing track of who approved whose leave. A company with 100 employees who need to prove they're compliant with Brunei's Employment Order. A company with 300 employees who are ready for a private database and an enterprise contract.

Circlate grows with them. The same software, the same interface, the same rules — just more capacity underneath as the company gets bigger.
