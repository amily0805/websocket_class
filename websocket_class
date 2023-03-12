import websocket


class web_conn:
    def __init__(self, ws_url, msgs=None, continue_msg=None, interval=None, fun=None):
        # 初始化服务器地址
        self.url = ws_url
        # 初始化消息列表
        if not isinstance(msgs, list):
            raise AttributeError('msgs参数必须是list类型')
        self.msgs = msgs
        # 初始化消息间隙, 以及统计收到消息数量
        self.interval = 6  # 默认值为6
        self.messageNum = 0
        if interval:
            self.interval = interval
        # 初始化持续消息
        self.continue_msg = continue_msg
        # 初始化解密函数
        self.fun = fun
        # 初始化websocket
        self.socket = websocket.WebSocketApp(
            self.url,
            on_message=self.on_message,
            on_error=self.on_error,
            on_close=self.on_close,
            on_open=self.on_open
        )

    def login(self):
        # 向服务器发送连接信息
        while self.msgs:
            m = self.msgs.pop()
            print('we sent: ' + m)
            self.socket.send(m)

    def on_message(self, ws, message):
        # 输出服务器推送过来的内容
        if self.fun:
            print(self.fun(message))
        else:
            print(message)
        # 保持连接继续向服务器发送请求
        self.messageNum += 1
        if self.continue_msg:
            if self.messageNum % self.interval == 0:
                self.socket.send(self.continue_msg)

    def on_error(self, ws, error):
        # 报错
        print('报错:', error)

    def on_close(self, ws, *args):
        # 关闭连接
        print("######## on_close ########")

    def on_open(self, *args):
        # 连接服务器
        self.login()
        print('####### on_connect #######')

    def run(self):
        # 运行循环
        self.socket.run_forever()
