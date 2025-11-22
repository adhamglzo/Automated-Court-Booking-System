# 🏸 Automated Court Booking & Cancellation System

This project is a robust, serverless solution developed using Google Apps Script to automate the entire court booking workflow for a residential area, ensuring fairness and enforcing cancellation policies.

---

## ✨ Project Highlights

This system solves several common administrative challenges by:

* **Serverless Architecture:** Built entirely on Google Workspace (Apps Script, Sheets, Forms, Calendar) for zero infrastructure cost and maintenance.
* **Atomic Cancellation:** Generates unique, one-time-use cancellation links (via a `doGet` function) that expire immediately upon use, preventing abuse or double-cancellation attempts.
* **Enforced Rules & Policies:** Code logic prevents same-day cancellations and validates booking times, eliminating manual error and disputes.
* **Unit ID Standardization:** Implements a custom function (`standardizeUnitID`) to convert user input into a standardized 6-digit unit ID format for reliable lookups against a defaulter list or booking history.

---

## ⚙️ Tech Stack & Architecture

This solution leverages the following components:

| Component | Technology | Role |
| :--- | :--- | :--- |
| **Backend Logic** | Google Apps Script (JavaScript) | Handles form submission, calendar interaction, and policy enforcement. |
| **Data Storage** | Google Sheets | Stores booking IDs, user information, and serves as a simple database. |
| **User Interface** | HTML Service (`ConfirmPage.html`, `SuccessPage.html`) | Custom web pages to provide a professional user experience for confirmation and status feedback. |
| **Primary Inputs** | Google Forms | Collects initial booking requests from users. |
| **Scheduling** | Google Calendar | Manages the official booking schedule and time conflicts. |

---

## 💻 Code Structure Overview

The repository consists of the following key files:

| File Name | Description | Key Functions/Purpose |
| :--- | :--- | :--- |
| `Code.gs` | **Main Backend Script.** Contains core logic for form submission processing, ID standardization, and checking for common booking conflicts. | `standardizeUnitID`, `onFormSubmit` |
| `CancellationScript.gs` | **Cancellation Handler.** Contains the logic that runs when a user clicks a cancellation link from their email. It performs the same-day check and handles event deletion. | `doGet`, `cancelEvent` |
| `ConfirmPage.html` | **Confirmation Page.** The user-facing page that displays booking details and asks for final confirmation before cancellation is executed. | Provides the crucial **"Yes, Cancel"** link that calls the script. |
| `SuccessPage.html` | **Success Page.** Displays a simple, positive message upon successful cancellation. | Confirms the booking has been deleted from the calendar. |
| `cancellationRejected.html` | **Error/Rejection Page.** Displays clear reasons if the cancellation request fails (e.g., same-day rule violation or invalid link). | Improves user experience by giving clear feedback on policy enforcement. |

---

## 🖼️ Example Interface

*(**Optional but highly recommended:** Replace the text below with actual screenshots of your running pages. You can upload images to your repo and link them using Markdown, for example, `![Cancellation Page](assets/cancellation_page_screenshot.png)`.)*

| Cancellation Confirmation | Cancellation Rejection |
| :---: | :---: |
| A screenshot of `ConfirmPage.html` would go here, showing the booking details and confirmation button. | A screenshot of `cancellationRejected.html` would go here, showing the error message and policy notes. |

---

## 🚀 Getting Started (Deployment)

1.  **Clone the Repository:** Download these files into your local directory.
2.  **Open Google Apps Script:** Create a new project in Google Apps Script.
3.  **Transfer Files:** Copy the content of the `.gs` files (`Code.gs`, `CancellationScript.gs`) into the Code Editor. Copy the content of the `.html` files into new HTML files (e.g., `ConfirmPage.html`, `SuccessPage.html`).
4.  **Configuration:** Update the `CALENDAR_ID` and `HARDCODED_SCRIPT_URL` variables within the `.gs` files to match your live deployment URL and calendar ID.
5.  **Deploy as Web App:** Deploy the script as a Web App (set execution to **'Me'** and access to **'Anyone'** or **'Anyone, even anonymous'** if used publicly).
