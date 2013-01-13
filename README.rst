Examples
========
*Documentation below*
The following is nothing more than connecting to the chat, idling in the room::

  import chatbot

	class MyBot(chatbot.ChatBot):
		"""
		This class inherites the chatbot
		"""

		def __init__(self, username, password, site):
			chatbot.ChatBot__init__(self,
						username,
						password,
						site)


	if __name__ == '__main__':
		bot = MyBot("MyUsername", "MyPassword", "http://mywiki.wikia.com")
		bot.start()

To read the messages back to the user in terminal/command prompt, an event has to be used::

	import chatbot

	class MyBot(chatbot.ChatBot):

		def __init__(self, username, password, site):
			chatbot.ChatBot__init__(self,
						username,
						password,
						site)

		def on_message(self, c, e):
			"""
			c - connection/client
			e - event
			This is what we'll use to gather and send data
			"""
			print "%s: %s" % (e.user, e.text)

	if __name__ == '__main__':
		bot = MyBot("MyUsername", "MyPassword", "http://mywiki.wikia.com")
		bot.start

Replying multiple events in the chatroom, example being a kick and a ban::

	import chatbot

	class MyBot(chatbot.ChatBot):

		def __init__(self, username, password, site):
			chatbot.ChatBot__init__(self,
						username,
						password,
						site)

		def on_kick(self, c, e):
			c.send("Oh dear!")

		def on_ban(self, c, e):
			c.send("Oh no! This is not good!")

	if __name__ == '__main__':
		bot = MyBot("MyUsername", "MyPassword", "http://mywiki.wikia.com")
		bot.start()

Documentation
=============

Below is the documentation for setting up and using the chatbot module.  To see a basic chatbot for
better understanding of the documentation, please refer to the examples.

Requirements
----------

To use this, there is one requirement:

* `requests <http://docs.python-requests.org/en/latest/>`_

The easiest way to install requests, is through the `Python Package Index`_,
so you can install the latest release with ``pip install requests``. 

If you don't have pip, `get pip`_!

.. _Python Package Index: http://pypi.python.org
.. _get pip:              http://pypi.python.org/pypi/pip

Installing
----------

Installing chatbot is very simple, if using pip (see above).  If using windows, 
open up cmd.exe/command prompt and execute ``pip install chatbot``.  If using Mac OS X,
it is similar to this, but run in terminal.  Execute ``pip install chatbot`` in terminal.

To make sure the installation worked, execute the following in your cmd.exe/terminal window:

.. image:: https://raw.github.com/hairr/chatbot/master/_images/confirm.png

If you received an error, try executing the pip command again/make sure you successfully installed pip.

Setting up
----------

To first begin your script, you'll need to import the module::

	import chatbot

From here, you'll need to inherit the class into your bot's class.::

	class MyBot(chatbot.ChatBot):

Now, you'll need to set up the initalizing parts in the class, this will connect the bot.::

	class MyBot(chatbot.ChatBot):
		def __init__(self):
			chatbot.ChatBot.__init__(self, "username", "password", "http://wiki.wikia.com")

After this, the bot has to be started.  Starting is very simple to do when
executing the file::
	
	if __name__ == '__main__':
		bot = MyBot()
		bot.start()

The complete file, without any other data, should look like so::

	import chatbot

	class MyBot(chatbot.ChatBot):
		def __init__(self):
			chatbot.ChatBot.__init__(self, "username", "password", "http://wiki.wikia.com")

	if __name__ == '__main__':
		bot = MyBot()
		bot.start()

Now, you might be thinking: "Where did start() come from?"  It comes from the inherited class.  It gathers all the instances in the MyBot class (see below), as well as the data specified to run the bot.  So, it's very important to include that data!

If you're worried of privacy when putting the password down, please know: There is **no** way of knowing the information.  It is all stored on your computer and is sent to the wiki to login (exactly the same way you log into the wiki).

Instances
---------
In the chat, users can send message, go away, kick another user, etc.  The following are
the instances, so an action be performed as a result.  For better understanding of how to
include the instances, please see the examples page.

On a message::

	def on_message(self, c, e):
		"""
		When a message is sent by a user, anything here will be performed.
		"""
		pass

When a user joins the chat::

	def on_join(self, c, e):
		"""
		When a user joins the chat, anything here will be performed.
		"""
		pass

When a user leaves the chat::

	def on_leave(self, c, e):
		"""
		When a user leaves the chat, anything here will be performed.
		"""
		pass

When a user goes "away" in chat::

	def on_away(self, c, e):
		"""
		When a user goes away in chat, anything here will be performed.
		"""
		pass

When a user comes back from being "away" in chat::

	def on_back(self, c, e):
		"""
		When a user comes back from being away in chat, anything here will be performed.
		"""
		pass

When a user is kicked from chat::

	def on_kick(self, c, e):
		"""
		When a user is kicked from chat, anything here will be performed.
		"""
		pass

When a user is banned from chat::

	def on_ban(self, c, e):
		"""
		When a user is banned from chat, anything here will be performed.
		"""
		pass

When a user is given chat moderator rights from chat::

	def on_chatmod(self, c, e):
		"""
		When a user is given the chat moderator rights in chat, anything here will be performed.
		"""
		pass

When the bot joins the chat::

	def on_welcome(self, c, e):
		"""
		When the bot joins the chat, anything here will be performed.
		"""
		pass

Connection/Client
-----------------

After connecting to the chatroom, there are several connection commands that will
allow a user/bot to perform actions.

.. function:: c.send(message)
	
	Sends a message to the chatroom

	:param message: Message to be sent

.. function:: c.go_away()

	Goes "away" in the chatroom, as the bot will not go "away" by default

.. function:: c.come_back()

	Comes back from the chat room, after being away

.. function:: c.kick_user(user)

	Kicks a user from the chatroom

	:param user: User to kick
	.. note::
		If the user/bot does not have the chatmoderator right, a kick will not preform.

.. function:: c.ban_user(user[, time=3600[, reason="Misbehaving in chat"]])
	
	Bans a user from the chatroom.

	:param user: User to ban
	:param time: Time of ban, in seconds
	:param reason: Reason of the ban
	:type time: integer
	:type reason: string
	.. note::
		if the user/bot does not have the chatmoderator right, a ban will not preform

.. function:: c.end_ban(user[, reason="Ending chat ban"])

	Ends a chatban for a user

	:param user: User to unban
	:param reason: Reason of the unbanning
	:type reason: string
	.. note::
		If the user/bot does not have the chatmoderator right, the ban can not be ended

.. function:: c.give_chatmod(user)

	Gives the chatmoderator right to a user.

	:param user: User to give the chat moderator right to

	.. note::
			If the user/bot does not have the sysop right, the chatmoderator right can not be given
Events
---------
In the chat room, there are few events that can be gathered for information

.. data:: e.user

	Retrieves the user of the event.

	Note: ``on_kick``, ``on_chatmod`` and ``on_ban`` return arrays with the users involved.

	:rtype: string

.. data:: e.text

	Retrieves the text from the message.

	:rtype: string or None

.. data:: e.status

	Retrieves the status of the user for ``on_away`` and ``on_back``.

	:rtype: string or None
