Here is a simple _**Slack_Notify**_ to send updates about actions done on a github repository to particular channels on Slack. 
This step by step guide will help you to enable this GitHub action without the Slack API Key. 

STEPS: 
1. Start by creating a file in .github/workflows/slack-notify.yml file in your GitHub repo.

2. The following code should be added to the file slack-notify.yml file.
```
	on: push
	name: Slack Notification Demo
	jobs:
		slackNotification:
			name: Slack Notification
			runs-on: ubuntu-latest
			steps:
			- uses: actions/checkout@v2
			- name: Slack Notification
			  uses: rtCamp/action-slack-notify@master
			  env:
				SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
```
				
3. Now a SLACK_WEBHOOK secret needs to be created  using the GitHub Action's Secret. 
   _A webhook is similar to an API which is used to send real-time information such a changes made to a project from one application to another._
   
   The [generation of Slack Webhook](https://slack.com/apps/A0F7XDUAZ-incoming-webhooks) helps customise where and what needs to be send to Slack. For instance, it helps select the Channel or individual person who needs to be notified. The icon, label, message to be displayed are some instances of what can be customised in the Slack Webhook Settings.

4. Once the Webhook is created, paste it in Your_repo/Settings/Secrets.

5. By default, the action can run with minimal configuration settings but they can be customised using the following environment variables. 
	| Variable | Default | Purpose |
	|----------|-----------|----------|
	| SLACK_CHANNEL | Set during Slack webhook creation | Specify Slack channel in which message needs to be sent |
	| SLACK_USERNAME | ![rtBot](https://avatars0.githubusercontent.com/u/43742164?s=32&v=4) | The name of the sender of the message. Does not need to be a "real" username |
	| SLACK_ICON | rtBot Avatar | User/Bot icon shown with Slack message. It uses the URL supplied to this env variable to display the icon in slack message. |
	| SLACK_ICON_EMOJI |  -  | User/Bot icon shown with Slack message, in case you do not wish to add a URL for slack icon as above, you can set slack emoji in this env variable. Example value: :bell: or any other valid slack emoji. |
	| SLACK_COLOR | good (green) | 	You can pass an RGB value like #efefef which would change color on left side vertical line of Slack message. |
	| SLACK_MESSAGE | Generated from git commit message. | The main Slack message in attachment. It is advised not to override this. |
	| SLACK_TITLE | Message | Title to use before main Slack message. |
	| SLACK_FOOTER | Powered By rtCamp's GitHub Actions Library | Slack message footer. |
	| MSG_MINIMAL |  -  | If set to true, removes: Ref, Event and Actions URL from the message. |

	Usage:
	```
		- name: Slack Notification
      	  uses: rtCamp/action-slack-notify@master
      	  env:
      	  SLACK_CHANNEL: general
      	  SLACK_COLOR: '#3278BD'
      	  SLACK_ICON: https://github.com/rtCamp.png?size=48
      	  SLACK_MESSAGE: 'Post Content'
      	  SLACK_TITLE: Post Title
      	  SLACK_USERNAME: rtCamp
      	  SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
	``` 

By using this method, whatever commits are performed on github, will be notified on the **#general** channel of Slack with the username **rtCamp** and the message will be **Post Content**.