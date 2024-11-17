# Easy-Unsubscribe-All-Youtube
This is a script that unsubscribe all Youtube subscription. 


```
(async () => {
    const sleep = (ms) => new Promise(resolve => setTimeout(resolve, ms));

    // Get all subscription buttons on the page
    const subscribeButtons = document.querySelectorAll('ytd-subscribe-button-renderer button');

    for (const button of subscribeButtons) {
        if (button.innerText.toLowerCase().includes('subscribed')) {
            button.click(); // Open the menu
            await sleep(500); // Wait for the menu to appear

            // Find the exact "Unsubscribe" option
            const unsubscribeOption = Array.from(document.querySelectorAll('tp-yt-paper-item'))
                .find(item => item.innerText.trim().toLowerCase() === 'unsubscribe');

            if (unsubscribeOption) {
                unsubscribeOption.click(); // Click the unsubscribe option
                await sleep(500); // Wait for the confirmation dialog to appear

                // Find the confirmation button in the pop-up
                const confirmButton = document.querySelector('yt-button-renderer#confirm-button button');
                if (confirmButton) {
                    confirmButton.click(); // Click to confirm unsubscribe
                    console.log("Unsubscribed successfully!");
                } else {
                    console.error("Confirm button not found.");
                }
            }

            await sleep(1000); // Wait before moving to the next channel
        }
    }
})();
```
