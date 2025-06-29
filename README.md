# CherryTree RPG Wishing Well Tracker (Google Sheets)

## Overview

This repository showcases a highly popular and community-adopted Google Sheets-based tracker designed for players of the mobile idle RPG, "CherryTree - Text RPG." The tracker utilizes advanced spreadsheet formulas to help players efficiently monitor their progress with the in-game Wishing Well feature, optimize their strategy for obtaining permanent stat buffs, and track their journey to maximize this valuable game mechanic. This tool prioritizes ease of use through thoughtful design and robust error handling.

## Problem Solved

In "CherryTree - Text RPG," the Wishing Well provides permanent stat buffs in exchange for in-game gold coins, but its progression is often opaque, making it difficult for players to track their progress, know how many wishes they have left, or how much more gold they need to complete their wishing well. Manual tracking is cumbersome and prone to errors, leading to inefficient gameplay. The need arose for a clear, automated tool to guide players through this critical game feature.

## Solution & Key Features

This Google Sheets solution provides a comprehensive and interactive tool for Wishing Well optimization, designed with a focus on user experience and robust data integrity:

* **Core Data Table (Rarity & Rewards):** The main interface features an 8-column table (with one column hidden for troubleshooting) that organizes wish rewards by rarity.
    * **Visual Cues:** Rows are highlighted based on reward rarity: Common (yellow), Rare (green), Epic (blue), and Legendary (purple), providing immediate visual organization.
    * **Reward Details:** Displays various wish rewards (e.g., Attack, Archery, Global exp) with their descriptions and maximum "Cap" levels.
* **Intuitive User Input:**
    * **Dedicated Input Column:** A visually distinct column (a slightly darker shade of its respective rarity rank with a thick border) is designated for user input, where players enter their current levels for each reward.
    * **Explicit Guidance:** A clear note highlighted in red ("Only input information into Cells E5 through E23. This sheet is designed so that you only have to put your levels into those cells. Changing any other cells may cause some functionality to be lost") prevents accidental modification of underlying formulas, significantly enhancing ease of use.
* **Advanced Formula-Driven Logic & Error Handling:**
    * **Remaining Levels Calculation:** A formula dynamically calculates how many levels remain for each reward (`Cap - Current Level`), instantly updating as the user progresses. This calculation is protected by **multi-layered error checking** to ensure input validity.
    * **Calculated Stat Buffs:** Displays the effective stat buff for each reward based on the player's current level, providing clear and unambiguous feedback (e.g., "+ 100 Archery Damage"). This calculation intelligently bypasses if input errors are detected in the "Remaining" column.
    * **Dynamic Troubleshooting Column:** An 8th, initially invisible, column serves as a dedicated **troubleshooting and feedback mechanism**. It only becomes visible (along with its header) for rows where invalid user input is detected.
        * **Specific Error Messages:** Provides clear, actionable error messages (e.g., "For Current Level, please enter a whole number between 0 and [Cap]. No decimals.", "Please enter a numeric value for Current Level").
        * **Humorous Fallback:** Includes a lighthearted "ERROR 3" message for unexpected input, adding personality to the user experience.
    * **Example Formulas from the Sheet:**
        * **Remaining (e.g., F9 for "Archery"):**
            ```excel
            =IFERROR(IF(ISNUMBER(E9),IF(E9>=0,IF(E9<=D9,IF(MOD(E9,1)=0,IF(D9-E9<>0,D9-E9,"MAX LEVEL"),"ERROR 1"),"ERROR 1"),"ERROR 1"),IF(ISBLANK(E9),D9,"ERROR 2")),"ERROR 3")
            ```
            * *Explanation:* This formula meticulously validates user input (`E9`) ensuring it's a non-negative whole number within the defined `Cap` (`D9`). It provides specific error codes (`ERROR 1`, `ERROR 2`) for different invalid inputs or displays "MAX LEVEL" when a buff is capped. The outer `IFERROR` acts as a robust catch-all.
        * **Current Bonus Totals (e.g., G9 for "Archery"):**
            ```excel
            =IFERROR(IF(LEFT(F9,5)<>"ERROR","+ " & E9*2 & " Archery Damage",""),"")
            ```
            * *Explanation:* This formula intelligently checks if the `Remaining` column (`F9`) has an error. If `F9` does not contain an "ERROR" message, it calculates and displays the effective stat buff (e.g., `Current Level * 2` for Archery) in a user-friendly format. Otherwise, it remains blank to prevent cascading incorrect information.
        * **Troubleshooting (e.g., H9 for "Archery"):**
            ```excel
            =IF(F9="ERROR 1","For Current Level, please enter a whole number between 0 and " & D9 & ". No decimals.", IF(F9="ERROR 2","Please enter a numeric value for Current Level",IF(F9="ERROR 3","I only factored in two types of error here. Do better.","")))
            ```
            * *Explanation:* This formula provides contextual and actionable feedback to the user based on the error code returned by the `Remaining` column, guiding them to correct their input. It even includes a touch of humor for extremely unexpected inputs.
* **Actionable Summary Metrics:** Directly below the table, a small section summarizes total "wishes left" and calculates the "gold needed to max out" the entire Wishing Well, providing clear progression goals for the player.

## Impact & Results

This Wishing Well Tracker has benefited the CherryTree RPG community by:

* **Enhancing Player Experience:** Provided a clear, automated method for tracking a complex game mechanic, reducing player frustration and improving engagement.
* **Facilitating Resource Understanding:** Helped players understand their progress towards completing the Wishing Well and the total gold investment required, regardless of the randomness of individual buff draws.
* **Fostering Community Engagement:** Became a shared resource within the Discord server, facilitating discussion and collaborative optimization strategies among players.
* **Showcasing Analytical Prowess:** Demonstrates the ability to apply analytical and logical problem-solving skills to diverse data challenges, even in a recreational context.

## Technologies Used

* **Google Sheets:** Advanced Formulas (`IFERROR`, `IF`, `ISNUMBER`, `ISBLANK`, `MOD`, `LEFT`, `SUM`, Logical Functions), Conditional Formatting, Data Validation.

## Getting Started / How to Use

1.  **Access the Tracker:**
    * This project is implemented as a Google Sheet. While the file isn't directly hosted here on GitHub, you can [**access a view-only version of the anonymized tracker here**](LINK_TO_VIEW_ONLY_GOOGLE_SHEET_WITH_DUMMY_DATA).
2.  **Make a Copy:** To use the tracker yourself, simply open the link above and go to `File > Make a copy` to create your own editable version in your Google Drive.
3.  **Input Your Data:** Navigate to the designated input cells in **Column E** (specifically cells E5 through E23). Enter your current levels for each reward.
4.  **View Progress & Insights:** The tracker will automatically update to show your current Wishing Well progress, next buff milestones, and optimal gold contribution strategy. The troubleshooting column will dynamically appear if invalid input is detected.

## Anonymization Note

The provided view-only Google Sheet contains dummy data to demonstrate the tracker's full functionality while protecting any personal game progress data. The underlying formulas and logic remain completely intact.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
