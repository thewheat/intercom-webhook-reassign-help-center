# Intercom Webhook Reassign Help Center Conversations
- This is [Intercom webhook](https://docs.intercom.io/integrations/webhooks) processing code to 
   - reassign conversations to a custom admin/inbox instead of Unassigned 
   - when conversations are started from an article page your [Educate Help Center](https://docs.intercom.com/educating-your-customers/get-started/how-intercom-educate-works#make-articles-discoverable-on-your-help-center-)
   - Reassignment is done via the [Intercom API](https://developers.intercom.io/reference)
- Currently conversations started on an article page are considered replies to a conversation instead of a new conversation and do not get processed via [Assignment Rules](http://docs.intercom.io/Intercom-for-customer-support/assignment-rules)
- With this code you can reassign these conversations to a custom admin / team inbox


## Setup - Environment Variable Configuration
- lists all variables needed for this script to work
- `TOKEN`
	- Requires an extended access token to read conversation to identify if it is from the help center
	- Apply for an access token  https://app.intercom.io/developers/_
	- Read more about access tokens https://developers.intercom.com/reference#personal-access-tokens-1 
- `assignee_admin_id`
	- the ID of the teammate or inbox to reassign conversations to 
	- retrieve IDs via Admin API https://developers.intercom.io/reference#admins
- `bot_admin_id`
	- the ID of the admin that performs the reassignment (must be an admin not a team)
- For development just rename `.env.sample` to `.env` and modify values appropriately

## Running this locally

```
gem install bundler # install bundler
bundle install      # install dependencies
ruby app.rb         # run the code
ngrok http 4567     # uses https://ngrok.com/ to give you a public URL to your local code to process the webhooks
```

- Create a new webhook in the [Intercom Developer Hub](https://app.intercom.io/developers/_) > Webhooks page
- Listen on the following notification: "Reply from a user or lead" / `conversation.user.replied`
- In webhook URL specify the ngrok URL

