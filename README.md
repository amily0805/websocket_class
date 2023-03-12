# websocket_class
this is a websocket class, easy using in crawl
# params
there is the params list
url --> ws connect url (must provide)
msgs --> the start conversation list (must provide, and must be list)
continuue_msg --> some connect need continue push msg, this is the message (optional)
interval --> the interval of continue message
fun --> some messages are encrypted, this param you need provide a funtion to decrypt message
# usage
instantiation a class object WS
WS.run()
