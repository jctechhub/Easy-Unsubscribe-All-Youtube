# Easy-Unsubscribe-All-Youtube

If you have hundreds of subscriptions in Youtube, and you want to easily unsubcribe all of them, do the following: 

## Open YouTube on your desktop and go to your Subscriptions page:
https://www.youtube.com/feed/channels.

## Open the Browser Console:

On Chrome: Press Ctrl + Shift + J (Windows) or Cmd + Option + J (Mac).     
On Firefox: Press Ctrl + Shift + K (Windows) or Cmd + Option + K (Mac).

## Copy and Paste the Script Below into the console and press Enter:

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

The code will simulate the button click of the 'Unsubcribe' button:      
<img width="209" alt="image" src="https://github.com/user-attachments/assets/38e8c157-791a-4ad3-b56c-9fb8697f10e7">


# If error like following: 
<img width="411" alt="image" src="https://github.com/user-attachments/assets/d179d9a5-cb22-4492-ac75-2b1af31b2e12">           
     
Just open incognitor mode in chrome or private window in Edge, login Youtube, and repeat above. 
