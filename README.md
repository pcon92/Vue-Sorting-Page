# Vue Sorting Page

Live on Netlify - https://vue-sorting-page.netlify.app/

-   Built alongside Udemy Course Vue - The Complete Guide by Maximilian Schwarzmuller
-   Originally built with Vue Script import then remade with Vue CLI
-   Refactored separate components Bubble sort and Insertion sort into one Sorting card component
-   Once discovered Vue Style Guide refactor to fit style guide (e.g. prop definitions including types)
-   Deployed initial version (to practice deploment) alongside 'Optimizing & Deploying Vue Apps' Udemy course section (as mentioned above).
-   Still needs further additions, particularly mobile responsive, footer, styling, descriptions, site information.

Recent updates:

-   Had problems using the branded package in Font Awesome (from npm install, unable to find github logo) so imported into index.html instead
-   Styled in the same color scheme as Vue
-   Added first mobile responsive CSS adjustments
-   Add ability to remove card from card itself and to scroll to new card on create

Bugs:

-   After removing one card on mobile the next card is 'hovered' over

---

Resources referenced:

-   For the 'await sleep' idea to help display sorting animations.

    -   The top answer on - https://stackoverflow.com/questions/951021/what-is-the-javascript-version-of-sleep - meagar/Dan Dascalescu

-   For Selection sort implementation

    -   https://stackabuse.com/selection-sort-in-javascript/ - Mila Lukic

-   For Shell sort implementation
    -   https://learnersbucket.com/tutorials/algorithms/shell-sort-algorithm-in-javascript/ - Prashant Yadav
