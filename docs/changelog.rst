:orphan:

Changelog
=========

****************
Version 3.3.0
****************

- Added new event to Chat: :const:`~twitchAPI.types.ChatEvent.MESSAGE_DELETE` which triggers whenever a single message got deleted in a channel
- Added :const:`~twitchAPI.chat.Chat.send_raw_irc_message()` method for sending raw irc commands to the websocket. Use with care!
- Fixed missing state cleanup after closing Chat, preventing the same instance from being started again
- fixed :const:`~twitchAPI.types.ChatRoom.room_id` always being Null

****************
Version 3.2.2
****************

- Fixed return type of :const:`~twitchAPI.twitch.Twitch.get_broadcaster_subscriptions()`
- removed any field starting with underscore from :const:`~twitchAPI.object.TwitchObject.to_dict()`

****************
Version 3.2.1
****************

- Fixed bug that resulted in a timeout when reading big API requests
- Optimized the use of Sessions, slight to decent performance optimization for API requests, especially for async generators

****************
Version 3.2.0
****************

- Made the used loggers available for easy logging configuration
- added the option to set the chat command prefix via :const:`~twitchAPI.chat.Chat.set_prefix()`
- :const:`~twitchAPI.twitch.Twitch.set_user_authentication()` now also throws a :const:`~twitchAPI.types.MissingScopeException` when no scope is given. (thanks `@aw-was-here <https://github.com/aw-was-here>`_!)


****************
Version 3.1.1
****************

- Added the Endpoint "Get Chatters" :const:`~twitchAPI.twitch.Twitch.get_chatters()`
- Added the :const:`~twitchAPI.types.AuthScope.MODERATOR_READ_CHATTERS` AuthScope
- Added missing :const:`total` field to :const:`~twitchAPI.twitch.Twitch.get_users_follows()`
- added :const:`~twitchAPI.chat.ChatCommand.send()` shorthand to ChatCommand, this makes sending command replies easier.
- Fixed issue which prevented the Twitch client being used inside a EventSub, PubSub or Chat callback
- Fixed issue with using the wrong API url in :const:`~twitchAPI.twitch.Twitch.create_custom_reward()`
- :const:`twitchAPI.helper.first()` now returns None when there is no data to return instead of raising StopAsyncIteration exception
- Exceptions in Chat callback methods are now properly displayed

****************
Version 3.0.1
****************

- Fixed bug which resulted in :code:`Timeout context manager should be used inside a task` when subscribing to more than one EventSub topic

****************
Version 3.0.0
****************

.. note:: This Version is a major rework of the library. Please see the :doc:`v3-migration` to learn how to migrate.

**Highlights**

- Library is now fully async
- Twitch API responses are now Objects and Generators instead of pure dictionaries
- Automatic Pagination of API results
- First alpha of a Chat Bot implementation
- More customizability for the UserAuthenticator
- A lot of new Endpoints where added
- New look and content for the documentation

**Full Changelog**

* Rewrote the twitchAPI to be async
* twitchAPI now uses Objects instead of dictionaries
* added automatic pagination to all relevant API endpoints
* PubSub now uses async callbacks
* EventSub subscribing and unsubscribing is now async
* Added a alpha version of a Twitch Chat Bot implementation
* switched AuthScope `CHANNEL_MANAGE_CHAT_SETTINGS` to `MODERATOR_MANAGE_CHAT_SETTINGS`
* Added the following AuthScopes:

  * :const:`~twitchAPI.types.AuthScope.MODERATOR_MANAGE_ANNOUNCEMENTS`
  * :const:`~twitchAPI.types.AuthScope.MODERATOR_MANAGE_CHAT_MESSAGES`
  * :const:`~twitchAPI.types.AuthScope.USER_MANAGE_CHAT_COLOR`
  * :const:`~twitchAPI.types.AuthScope.CHANNEL_MANAGE_MODERATORS`
  * :const:`~twitchAPI.types.AuthScope.CHANNEL_READ_VIPS`
  * :const:`~twitchAPI.types.AuthScope.CHANNEL_MANAGE_VIPS`
  * :const:`~twitchAPI.types.AuthScope.USER_MANAGE_WHISPERS`
* added :const:`~twitchAPI.helper.first()` helper function

* Added the following new Endpoints:

  * "Send Whisper" :const:`~twitchAPI.twitch.Twitch.send_whisper()`
  * "Remove Channel VIP" :const:`~twitchAPI.twitch.Twitch.remove_channel_vip()`
  * "Add Channel VIP" :const:`~twitchAPI.twitch.Twitch.add_channel_vip()`
  * "Get VIPs" :const:`~twitchAPI.twitch.Twitch.get_vips()`
  * "Add Channel Moderator" :const:`~twitchAPI.twitch.Twitch.add_channel_moderator()`
  * "Remove Channel Moderator" :const:`~twitchAPI.twitch.Twitch.remove_channel_moderator()`
  * "Get User Chat Color" :const:`~twitchAPI.twitch.Twitch.get_user_chat_color()`
  * "Update User Chat Color" :const:`~twitchAPI.twitch.Twitch.update_user_chat_color()`
  * "Delete Chat Message" :const:`~twitchAPI.twitch.Twitch.delete_chat_message()`
  * "Send Chat Announcement" :const:`~twitchAPI.twitch.Twitch.send_chat_announcement()`
  * "Get Soundtrack Current Track" :const:`~twitchAPI.twitch.Twitch.get_soundtrack_current_track()`
  * "Get Soundtrack Playlist" :const:`~twitchAPI.twitch.Twitch.get_soundtrack_playlist()`
  * "Get Soundtrack Playlists" :const:`~twitchAPI.twitch.Twitch.get_soundtrack_playlists()`
* Removed the folllowing deprecated Endpoints:

  * "Get Banned Event"
  * "Get Moderator Events"
  * "Get Webhook Subscriptions"
* The following Endpoints got changed:

  * Added `igdb_id` search parameter to :const:`~twitchAPI.twitch.Twitch.get_games()`
  * Removed the Voting related fields in :const:`~twitchAPI.twitch.Twitch.create_poll()` due to being deprecated
  * Updated the logic in :const:`~twitchAPI.twitch.Twitch.update_custom_reward()` to avoid API errors
  * Removed `id` parameter from :const:`~twitchAPI.twitch.Twitch.get_hype_train_events()`
  * Fixed the range check in :const:`~twitchAPI.twitch.Twitch.get_channel_information()`
* :const:`~twitchAPI.twitch.Twitch.app_auth_refresh_callback` and :const:`~twitchAPI.twitch.Twitch.user_auth_refresh_callback` are now async
* Added :const:`~twitchAPI.oauth.get_user_info()`
* UserAuthenticator:

  * You can now set the document that will be shown at the end of the Auth flow by setting :const:`~twitchAPI.oauth.UserAuthenticator.document`
  * The optional callback is now called with the access and refresh token instead of the user token
  * Added browser controls to :const:`~twitchAPI.oauth.UserAuthenticator.authenticate()`
* removed :code:`requests` and :code:`websockets` libraries from the requirements (resulting in smaller library footprint)


****************
Version 2.5.7
****************

- Fixed the End Poll Endpoint
- Properly define terminated poll status (thanks @iProdigy!)

****************
Version 2.5.6
****************

- Updated Create Prediction to take between 2 and 10 outcomes (thanks @lynara!)
- Added "Get Creator Goals" Endpoint (thanks @gitagogaming!)
- TwitchAPIException will now also include the message from the Twitch API when available

****************
Version 2.5.5
****************

- Added datetime parsing to `created_at` field for Ban User and Get Banned Users endpoints
- fixed title length check failing if the title is None for Modify Channel Information endpoint (thanks @Meduris!)

****************
Version 2.5.4
****************

- Added the following new endpoints:

  - "Ban User"

  - "Unban User"

  - "Get Blocked Terms"

  - "Add Blocked Term"

  - "Remove Blocked Term"

- Added the following Auth Scopes:

  - `moderator:manage:banned_users`

  - `moderator:read:blocked_terms`

  - `moderator:manage:blocked_terms`

- Added additional debug logging to PubSub
- Fixed KeyError when being rate limited

****************
Version 2.5.3
****************

- `Twitch.get_channel_info` now also optionally accepts a list of strings with up to 100 entries for the `broadcaster_id` parameter

****************
Version 2.5.2
****************

- Added the following new endpoints:

  - "Get Chat Settings"

  - "Update Chat Settings"

- Added Auth Scope "channel:manage:chat_settings"
- Fixed error in Auth Scope "channel:manage:schedule"
- Fixed error in Endpoint "Get Extension Transactions"
- Removed unusable Webhook code

****************
Version 2.5.1
****************

- Fixed bug that prevented EventSub subscriptions to work if main threads asyncio loop was already running

****************
Version 2.5.0
****************

- EventSub and PubSub callbacks are now executed non blocking, this fixes that long running callbacks stop the library to respond to heartbeats etc.
- EventSub subscription can now throw a TwitchBackendException when the API returns a Error 500
- added the following EventSub topics (thanks d7415!)

  - "Goal Begin"

  - "Goal Progress"

  - "Goal End"

****************
Version 2.4.2
****************

- Fixed EventSub not keeping local state in sync on unsubscribe
- Added proper exception if authentication via oauth fails

****************
Version 2.4.1
****************

- EventSub now uses a random 20 letter secret by default
- EventSub now verifies the send signature

****************
Version 2.4.0
****************

- **Implemented EventSub**

- Marked Webhook as deprecated

- added the following new endpoints

  - "Get Followed Streams"

  - "Get Polls"

  - "End Poll"

  - "Get Predictions"

  - "Create Prediction"

  - "End Prediction"

  - "Manage held AutoMod Messages"

  - "Get Channel Badges"

  - "Get Global Chat Badges"

  - "Get Channel Emotes"

  - "Get Global Emotes"

  - "Get Emote Sets"

  - "Delete EventSub Subscription"

  - "Get Channel Stream Schedule"

  - "Get Channel iCalendar"

  - "Update Channel Stream Schedule"

  - "Create Channel Stream Schedule Segment"

  - "Update Channel Stream Schedule Segment"

  - "Delete Channel Stream Schedule Segment"

  - "Update Drops Entitlements"

- Added the following new AuthScopes

  - USER_READ_FOLLOWS

  - CHANNEL_READ_POLLS

  - CHANNEL_MANAGE_POLLS

  - CHANNEL_READ_PREDICTIONS

  - CHANNEL_MANAGE_PREDICTIONS

  - MODERATOR_MANAGE_AUTOMOD

  - CHANNEL_MANAGE_SCHEDULE

- removed deprecated Endpoints

  - "Create User Follows"

  - "Delete User Follows"

- Added Topics to PubSub

  - "AutoMod Queue"

  - "User Moderation Notifications"

- Check if at least one of status or id is provided in get_custom_reward_redemption
- reverted change that made reward_id optional in get_custom_reward_redemption
- get_extension_transactions now takes up to 100 transaction ids
- added delay parameter to modify_channel_information
- made parameter prompt of create_custom_reward optional and changed parameter order
- made reward_id of get_custom_reward take either a list of str or str
- made parameter title, prompt and cost optional in update_custom_reward
- made parameter redemption_ids of update_redemption_status take either a list of str or str
- fixed exception in block_user
- allowed Twitch.check_automod_status to take in more that one entry

****************
Version 2.3.2
****************

* fixed get_custom_reward_redemption url (thanks iProdigy!)
* made reward_id parameter of get_custom_reward_redemption optional

****************
Version 2.3.1
****************

* fixed id parameter for get_clips of Twitch

****************
Version 2.3.0
****************

* Initializing the Twitch API now automatically creates a app authorization (can be disabled via flag)
* Made it possible to not set a app secret in cases where only user authentication is required
* added helper function `validate_token` to OAuth
* added helper function `revoke_token` to OAuth
* User OAuth Token is now automatically validated for correct scope and validity when being set
* added new "Get Drops Entitlement" endpoint
* added new "Get Teams" endpoint
* added new "Get Chattel teams" endpoint
* added new AuthScope USER_READ_SUBSCRIPTIONS
* fixed exception in Webhook if no Authentication is set and also not required
* refactored Authentication handling, making it more versatile
* added more debugging logs
* improved documentation

****************
Version 2.2.5
****************

* added optional callback to Twitch for user and app access token refresh
* added additional check for non empty title in Twitch.modify_channel_information
* changed required scope of PubSub.listen_channel_subscriptions from CHANNEL_SUBSCRIPTIONS to CHANNEL_READ_SUBSCRIPTIONS


****************
Version 2.2.4
****************

* added Python 3.9 compatibility
* improved example for PubSub

****************
Version 2.2.3
****************

* added new "get channel editors" endpoint
* added new "delete videos" endpoint
* added new "get user block list" endpoint
* added new "block user" endpoint
* added new "unblock user" endpoint
* added new authentication scopes
* some refactoring

****************
Version 2.2.2
****************

* added missing API base url to delete_custom_reward, get_custom_reward, get_custom_reward_redemption and update_redemption_status (thanks asphaltschneider!)

****************
Version 2.2.1
****************

* added option to set a ssl context to be used by Webhook
* fixed modify_channel_information throwing ValueError (thanks asishm!)
* added default route to Webhook on / for easier debugging
* properly check for empty lists in the selection of the used AuthScope in get_users
* raise ValueError if both from_id and to_id are None in subscribe_user_follow of Webhook

****************
Version 2.2.0
****************

* added missing "Create custom rewards" endpoint
* added missing "Delete Custom rewards" endpoint
* added missing "Get Custom Reward" endpoint
* added missing "Get custom reward redemption" endpoint
* added missing "Update custom Reward" endpoint
* added missing "Update redemption status" endpoint
* added missing pagination parameters to endpoints that support them
* improved documentation
* properly handle 401 response after retries

****************
Version 2.1
****************

Added a Twitch PubSub client implementation.

See :doc:`modules/twitchAPI.pubsub` for more Info!

* added PubSub client
* made UserAuthenticator URL dynamic
* added named loggers for all modules
* fixed bug in Webhook.subscribe_subscription_events
* added Twitch.get_user_auth_scope

****************
Version 2.0.1
****************

Fixed some bugs and implemented changes made to the Twitch API

****************
Version 2.0
****************

This version is a major overhaul of the Webhook, implementing missing and changed API endpoints and adding a bunch of quality of life changes.

* Reworked the entire Documentation
* Webhook subscribe and unsubscribe now waits for handshake to finish
* Webhook now refreshes its subscriptions
* Webhook unsubscribe is now a single function
* Webhook auto unsubscribes from topics on stop()
* Added unsubscribe_all function to Webhook
* Twitch instance now auto renews auth token once they become invalid
* Added retry on API backend error
* Added get_drops_entitlements endpoint
* Fixed function signature of get_webhook_subscriptions
* Fixed update_user_extension not writing data
* get_user_active_extensions now requires User Authentication
* get_user_follows now requires at elast App Authentication
* get_users now follows the changed API Authentication logic
* get_stream_markers now also checks that at least one of user_id or video_id is provided
* get_streams now takes a list for game_id
* get_streams now checks the length of the language list
* get_moderator_events now takes in a list of user_ids
* get_moderators now takes in a list of user_ids
* get_clips can now use the first parameter
* Raise exception when twitch backend returns 503 even after a retry
* Now use custom exception classes
* Removed depraced endpoint get_streams_metadata
