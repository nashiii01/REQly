# ReverseMarket: 5-Minute Interactive Demo Script

This script guides an evaluator or stakeholder through the complete ReverseMarket end-to-end loop in under 5 minutes.

---

## ⏱️ Minute 0:00 – 1:00: Buyer Posts a Requirement with Smart NLP
1. **Navigate to App**: Open `http://localhost:3000` (or click `Login` from the Landing Page).
2. **One-Click Login**: Click the **"Demo Buyer"** button to log in instantly as *Rajesh Sharma*.
3. **Go to Post Requirement**:
   - In the sidebar or top bar, click **"Post Requirement"** (or navigate to `/buyer/requirements/new`).
4. **Smart Natural Language Parser**:
   - In the Smart Requirement Parser card, click **"Load Example Prompt"** (or paste: `"Need 3 developer laptops with 32GB RAM, RTX GPU, 1TB SSD under ₹85,000 in 10 days"`).
   - Click **"Apply Extraction"**.
   - Notice how Category (*Computers*), Title (*Custom Laptop...*), Budget (*₹68,000 – ₹85,000*), Deadline, Quantity (*3*), and Preferences (*32GB RAM, 1TB NVMe SSD, Dedicated GPU*) are automatically populated into the form.
5. **Publish**:
   - Click **"Publish Requirement"**.
   - You are redirected to **My Requirements** where your new RFP is live and active.

---

## ⏱️ Minute 1:00 – 2:15: Provider Discovers RFP & Submits Competitive Proposal
1. **Switch Role**:
   - In the header top bar, click the **"Switch: Provider"** quick switcher button (or logout and click "Demo Provider").
   - You are now logged in as *Ananya Deshmukh (NextGen Systems & Tech)*.
2. **Browse Requirements**:
   - Click **"Browse Requirements"** in the sidebar (`/provider/requirements`).
   - Locate the newly published requirement at the top of the feed.
   - Click **"Inspect & Submit Offer"** (`/provider/requirements/:id`).
3. **Compatibility Preview & Bidding**:
   - Review the Compatibility Match Score preview.
   - Fill out the offer submission form:
     - **Proposed Price**: `₹82,000`
     - **Delivery Timeline**: Select date within 10 days
     - **Scope Description**: `"Enterprise ThinkPad P16s with 32GB RAM, 1TB NVMe SSD, RTX A500, and 3-Year On-Site Premier Support."`
     - **Inclusions**: `"Next-day shipping, GST Invoice"`
   - Click **"Submit Offer"**.
   - Confirm offer appears in the **My Proposals Pipeline** (`/provider/offers`).

---

## ⏱️ Minute 2:15 – 3:30: Buyer Reviews Matches, Compares, Chats & Awards Contract
1. **Switch Role**:
   - In the header top bar, click **"Switch: Buyer"**.
   - Notice the bell notification in the top right: *"New Offer Received from NextGen Systems & Tech"*.
2. **Match Center & Score Transparency**:
   - Click **"Match Center"** (`/buyer/matches`).
   - Inspect the **Match Score** (e.g. 92% Match).
   - Click **"Score Breakdown & Reasons"** to view transparent percentages for Relevance (35%), Budget Fit (25%), Delivery Fit (20%), Provider Trust (10%), and Offer Quality (10%).
3. **Shortlist & Compare**:
   - Click **"Shortlist"** on the proposal.
   - Click **"Compare"** (`/buyer/compare`) to inspect competing bids side-by-side with budget positions and feature highlights.
4. **Contextual Chat**:
   - Click the **"Message Provider"** button on the offer card.
   - Type `"Can you confirm that GST invoicing is included?"` and send.
5. **Select Winning Offer**:
   - Click **"Select Winning Offer"**.
   - Confirm the dialog. The requirement status transitions to **Awarded**, the offer transitions to **Selected**, and an active **Fulfillment Engagement** is created.

---

## ⏱️ Minute 3:30 – 4:15: Milestone Fulfillment & Verified 5-Star Review
1. **Track Milestones**:
   - You are in the **Selected Engagements & Milestones** view (`/buyer/selected`).
   - Switch to **Provider** role to advance milestones (e.g., *"Work started"*, *"Progress update"*, *"Delivery submitted"*).
2. **Accept Delivery & Release Payment**:
   - Switch back to **Buyer** role.
   - Click **"Accept Delivery & Sign Off"** on milestone 4.
   - Click **"Complete Engagement & Release Funds"** on milestone 5.
3. **Submit Verified Review**:
   - Click **"Leave Review & Rating"**.
   - Select **5 Stars**, check quality tags (*"On-Time"*, *"High Quality"*), write `"Flawless hardware delivery and prompt service!"`, and submit.
   - Click the provider's name to view their public trust profile (`/providers/usr-prov-1`) and verify the updated review count and rating.

---

## ⏱️ Minute 4:15 – 5:00: Admin Control Center & System Oversight
1. **Switch Role**:
   - In the header, click **"Switch: Admin"** (or logout and click "Demo Admin").
2. **Executive Control Center**:
   - View platform health KPIs on `/admin/dashboard` (Users, RFPs, Proposals, Active Contracts, GMV).
3. **User Governance & Safety Moderation**:
   - Click **"Users"** (`/admin/users`) -> Test suspending an account with reason -> observe instant login lock.
   - Click **"Reports"** (`/admin/reports`) -> Review incident queue -> Resolve report with resolution note.
4. **Dynamic Algorithm Tuning**:
   - Click **"Matching Config"** (`/admin/matching`) -> Adjust weight sliders (e.g., Increase Relevance to 40%) -> observe live score simulator -> Click Save.
5. **Immutable Audit Trail**:
   - Click **"Audit Log"** (`/admin/audit-log`) -> Verify all suspensions, status changes, and configurations are permanently recorded with timestamps and JSON payload inspectors.

---

### 🎉 Demo Complete!
The entire reverse-marketplace loop has been demonstrated end-to-end with persistent data, transparent scoring, and role-based permissions.
