# J. Kumar Infraprojects – IT Helpdesk System v2.0

**Developed by: Abhishek Tiwari | IT Professional**

---

## 📁 Files (Deploy ALL together)

| File | Purpose |
|------|---------|
| `index.html` | Main landing page with live stats |
| `employee_portal.html` | Employee ticket submission portal |
| `admin_portal.html` | IT Admin dashboard (ticket management) |
| `call_portal.html` | **NEW v2.0** – Engineer call report form |
| `call_admin.html` | **NEW v2.0** – Admin call reports panel |
| `call_report.html` | **NEW v2.0** – GM shareable report page |
| `favicon.svg` | J.Kumar browser tab icon |

---

## 🚀 GitHub Pages Deploy (Zero Data Loss)

```bash
# 1. Clone or init repo
git init
git remote add origin https://github.com/YOUR_USERNAME/jkumar-ithelpdesk.git

# 2. Add ALL files
git add index.html employee_portal.html admin_portal.html
git add call_portal.html call_admin.html call_report.html favicon.svg README.md

# 3. Commit & push
git commit -m "v2.0 - Call Report System added"
git push -u origin main

# 4. Enable GitHub Pages:
# GitHub Repo → Settings → Pages → Source: main branch → / (root)
```

**Your live URL:** `https://YOUR_USERNAME.github.io/jkumar-ithelpdesk/`

> ⚠️ **Data is in Firebase (cloud) — NOT in these HTML files.**
> Replacing/updating files on GitHub NEVER deletes any Firebase data.
> All tickets and call reports stay safe always.

---

## 🔥 Firebase Setup (One-time)

### Firestore Rules
Go to: **Firebase Console → Firestore → Rules** → paste:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /tickets/{doc} {
      allow read, write: if true;
    }
    match /call_reports/{doc} {
      allow read, write: if true;
    }
  }
}
```

### Storage Rules
Go to: **Firebase Console → Storage → Rules** → paste:

```
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write: if true;
    }
  }
}
```

### Firestore Indexes
Go to: **Firebase Console → Firestore → Indexes** → Add:

| Collection | Field 1 | Field 2 | Order |
|-----------|---------|---------|-------|
| `call_reports` | `callId` (ASC) | — | — |
| `call_reports` | `submittedAt` (DESC) | — | — |
| `tickets` | `createdAt` (DESC) | — | — |

---

## 🔐 Default Login Credentials

| Portal | Username | Password |
|--------|---------|---------|
| Admin Dashboard | `admin` | `jkumar123` |
| Call Portal (Engineer) | `admin` | `jkumar123` |
| Call Admin Panel | `admin` | `jkumar123` |

> Change passwords via: Admin Dashboard → IT Team → My Profile → Edit

---

## 📋 Call Report v2.0 — Features

- **5-step engineer form**: Call Info → Problem → Parts → Photos → Review
- **Parts/Components table**: Name, Qty, Action (Replaced/Installed/Repaired)
- **Purchase details**: PR Raised / Cash Purchase / AMC / Warranty
- **Image upload**: Up to 10 photos to Firebase Storage
- **Auto WhatsApp share** after submit with full details
- **GM shareable link**: `call_report.html?id=CALL-XXXXXXXX`
- **No login needed to VIEW** report link (GM can open directly)

---

## 📱 WhatsApp Share Format

When engineer submits, they get:
```
📋 J. Kumar Infraprojects – IT Call Report

🔖 Call ID: CALL-12345678
📅 Date: 05 May 2026
👤 Employee: Rahul Sharma
🏢 Dept: Accounts & Finance
🔧 Issue: Laptop not starting
✅ Status: Resolved
👷 Engineer: Abhishek Tiwari

🔗 Full Report: https://yoursite.github.io/call_report.html?id=CALL-12345678
```

---

## 🗄️ Firebase Data Structure

```
Firestore:
├── tickets/              ← IT Helpdesk tickets
│   └── {docId}
│       ├── ticketId, title, status, priority
│       ├── name, dept, phone, location
│       ├── timeline[], comments[]
│       └── rating, assignedName
│
└── call_reports/         ← Engineer Call Reports v2.0
    └── {docId}
        ├── callId, linkedTicketId
        ├── callDate, timeReceived, timeClosed
        ├── employeeName, employeePhone, department
        ├── location, assetTag, category, priority
        ├── problemTitle, problemDesc, rootCause
        ├── solution, timeTaken, resolutionMethod
        ├── partsUsed (bool), parts[]
        │   └── {name, qty, type, notes}
        ├── purchaseDone (bool)
        │   ├── purchaseType, prNumber, amount
        │   ├── vendorName, purchaseDate, approvedBy
        ├── vendorInvolved (bool), vendorCompany...
        ├── images[] → {name, url, type, size}
        ├── engineerName, engineerEmpId
        ├── finalComments, submittedAt
        └── version: "2.0"

Storage:
└── call_images/
    └── {callId}/
        └── {timestamp}_{filename}
```

---

## 📞 Contact
**Abhishek Tiwari** | IT Professional | J. Kumar Infraprojects Ltd.
