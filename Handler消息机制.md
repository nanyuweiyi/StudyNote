#### Handler消息机制

Android开发中使用该机制来进行消息的传递。

主要运用在UI线程和子线程，子线程和子线程之间传递消息。其中涉及到3个概念，Handler、Looper、MessageQueue. 首先MessageQueue是一个消息队列，
它是一个链表的结构，遵循先进先出的原则，Android通过Message对象发送消息到MessageQueue中。Looper是一个消息传递的运输工具，它主要负责运送Messagequeue
给handler去处理。Handler是一个消息接收并处理的平台，它接收消息并处理。








