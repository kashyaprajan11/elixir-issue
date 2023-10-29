Hi. I'm completely new to Elixir. I was following the hex docs while learning the framework. My application runs fine when I add the hello route. But as soon as I add /hello/:messenger route the whole /hello router crashed.
Basically when I called /hello router I get this error.
[error] #PID<0.533.0> running Phoenix.Endpoint.SyncCodeReloadPlug (connection #PID<0.532.0>, stream id 1) terminated
Server: localhost:4000 (http)
Request: GET /hello
** (exit) an exception was raised:
    ** (UndefinedFunctionError) function HelloWeb.HelloWeb.HelloController.init/1 is undefined (module HelloWeb.HelloWeb.HelloController is not available)
        HelloWeb.HelloWeb.HelloController.init(:index)
        (phoenix 1.7.9) lib/phoenix/router.ex:432: Phoenix.Router.__call__/5
        (hello 0.1.0) lib/hello_web/endpoint.ex:1: HelloWeb.Endpoint.plug_builder_call/2
        (hello 0.1.0) deps/plug/lib/plug/debugger.ex:136: HelloWeb.Endpoint."call (overridable 3)"/2
        (hello 0.1.0) lib/hello_web/endpoint.ex:1: HelloWeb.Endpoint.call/2
        (phoenix 1.7.9) lib/phoenix/endpoint/sync_code_reload_plug.ex:22: Phoenix.Endpoint.SyncCodeReloadPlug.do_call/4
        (plug_cowboy 2.6.1) lib/plug/cowboy/handler.ex:11: Plug.Cowboy.Handler.init/2
        (cowboy 2.10.0) /Users/roushankashyap/Desktop/Elixir/hello/deps/cowboy/src/cowboy_handler.erl:37: :cowboy_handler.execute/2
        (cowboy 2.10.0) /Users/roushankashyap/Desktop/Elixir/hello/deps/cowboy/src/cowboy_stream_h.erl:306: :cowboy_stream_h.execute/3
        (cowboy 2.10.0) /Users/roushankashyap/Desktop/Elixir/hello/deps/cowboy/src/cowboy_stream_h.erl:295: :cowboy_stream_h.request_process/3
        (stdlib 5.0.2) proc_lib.erl:241: :proc_lib.init_p_do_apply/3
I also checked phx.routes after and before defining the /hello/:messenger router. To my surprise there is a change.
Before defining:-
GET   /                                      HelloWeb.PageController :home
  GET   /hello                                 HelloWeb.HelloController :index
  GET   /dev/dashboard/css-:md5                Phoenix.LiveDashboard.Assets :css
  GET   /dev/dashboard/js-:md5                 Phoenix.LiveDashboard.Assets :js
  GET   /dev/dashboard                         Phoenix.LiveDashboard.PageLive :home
  GET   /dev/dashboard/:page                   Phoenix.LiveDashboard.PageLive :page
  GET   /dev/dashboard/:node/:page             Phoenix.LiveDashboard.PageLive :page
  *     /dev/mailbox                           Plug.Swoosh.MailboxPreview []
  WS    /live/websocket                        Phoenix.LiveView.Socket
  GET   /live/longpoll                         Phoenix.LiveView.Socket
  POST  /live/longpoll                         Phoenix.LiveView.Socket
After defining the /hello/:messenger route
 GET   /                                      HelloWeb.PageController :home
  GET   /hello                                 HelloWeb.HelloWeb.HelloController :index
  GET   /hello/:messenger                      HelloWeb.HelloWeb.HelloController :show
  GET   /dev/dashboard/css-:md5                Phoenix.LiveDashboard.Assets :css
  GET   /dev/dashboard/js-:md5                 Phoenix.LiveDashboard.Assets :js
  GET   /dev/dashboard                         Phoenix.LiveDashboard.PageLive :home
  GET   /dev/dashboard/:page                   Phoenix.LiveDashboard.PageLive :page
  GET   /dev/dashboard/:node/:page             Phoenix.LiveDashboard.PageLive :page
  *     /dev/mailbox                           Plug.Swoosh.MailboxPreview []
  WS    /live/websocket                        Phoenix.LiveView.Socket
  GET   /live/longpoll                         Phoenix.LiveView.Socket
  POST  /live/longpoll                         Phoenix.LiveView.Socket
I can see the /hello route changed from HelloWeb.HelloController to HelloWeb.HelloWeb.HelloContainer which is causing the error. Not sure how to resolve this or why this is happening.
P.S
Docs I'm using :- https://hexdocs.pm/phoenix/request_lifecycle.html
OS : MacOS