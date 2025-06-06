# Boots-Scoutdashboard
Private Dashboard 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Scout AI Assistant</title>
</head>
<body>
  <h1>Boots on the Ground - AI Assistant</h1>
  <p>Welcome to your AI-powered assistant. Let’s get to work!</p>

  <script>
    const SCOUT_CONFIG = {
      apiBase: 'https://boots-intelligence-1-taylordurling.replit.app/api',
      sendGridKey: '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',
      slackToken: 'xoxb-9013799810180-9025364012385-...',
      slackChannel: 'C0123456789'
    };

    async function sendAlert(subject, message) {
      try {
        const res = await fetch(`${SCOUT_CONFIG.apiBase}/email/send`, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({
            to: 'taylordurling@yahoo.com',
            subject,
            message
          })
        });
        const data = await res.json();
        console.log('Email sent:', data);
      } catch (err) {
        console.error('Email error:', err);
      }
    }

    async function notifySlack(message) {
      try {
        const res = await fetch(`${SCOUT_CONFIG.apiBase}/slack/notify`, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({
            token: SCOUT_CONFIG.slackToken,
            channel: SCOUT_CONFIG.slackChannel,
            message
          })
        });
        const data = await res.json();
        console.log('Slack notified:', data);
      } catch (err) {
        console.error('Slack error:', err);
      }
    }

    // Example use on page load
    window.onload = () => {
      sendAlert("Scout AI Booted", "The Assistant is live and ready.");
      notifySlack("👢 Boots on the Ground AI Assistant is now active!");
    };
  </script>
</body>
</html>
