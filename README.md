# Tmate GitHub Action Debug Demo

This repository demonstrates how to use the [Debugging with tmate](https://github.com/marketplace/actions/debugging-with-tmate) GitHub Action to debug failed workflows interactively.

## What is tmate?

Tmate is a terminal multiplexer that allows you to share terminal sessions over SSH or web browsers. In the context of GitHub Actions, it enables you to connect to a running workflow and debug issues in real-time.

## How to Use

### 1. Automatic Debugging on Failure

The workflow automatically starts a tmate session when any step fails. This happens because of the `if: ${{ failure() }}` condition on the tmate step.

### 2. Manual Debugging

You can also manually trigger debugging by:

1. Go to the **Actions** tab in your repository
2. Click on the **Debug with tmate - Simulated Failure** workflow
3. Click **Run workflow**
4. Check the **Run the build with tmate debugging enabled** checkbox
5. Click **Run workflow**

This will simulate a failure and start a tmate session for debugging.

### 3. Connecting to the Debug Session

When a tmate session starts, you'll see connection details in the workflow logs:

- **SSH connection**: Use the SSH command shown in the logs
- **Web terminal**: Click the web URL to open a browser-based terminal

### 4. Debugging Commands

Once connected, you can:

```bash
# Check the current state
pwd
ls -la
env | grep GITHUB

# Investigate the failure
cat .github/workflows/debug-with-tmate.yml
echo "Debugging the issue..."

# Continue the workflow when done
touch continue
# or on Linux: sudo touch /continue
```

### 5. Continuing the Workflow

To continue the workflow after debugging:

- Create a file named `continue` in the session
- On Linux runners: `sudo touch /continue`
- On other runners: `touch continue`

## Workflow Features

- **Simulated failures**: The workflow intentionally fails to demonstrate debugging
- **Conditional debugging**: Only starts tmate when needed
- **Security**: Uses `limit-access-to-actor: true` to restrict access to your SSH keys
- **Timeout**: 30-minute session timeout to prevent excessive resource usage
- **Manual trigger**: Can be manually run with debug mode enabled

## Security Notes

- The workflow uses `limit-access-to-actor: true` which means only users with registered SSH keys in their GitHub profile can connect
- Sessions automatically timeout after 30 minutes
- Only the workflow initiator can access the debug session

## Troubleshooting

If you can't see the connection string:
- Check the workflow logs every 5 seconds
- Look in the **Checks** tab of your PR
- Ensure you have SSH keys registered with your GitHub account

## Learn More

- [Debugging with tmate Action](https://github.com/marketplace/actions/debugging-with-tmate)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Tmate Documentation](https://tmate.io/)
