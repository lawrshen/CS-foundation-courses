# lesson1 multmedia

## Streaming, storedaudio, video

DASH

- streaming: can begin playout before downloading entire file

- stored (at server): can transmit faster than audio/video will be rendered (implies storing/buffering at client)

- e.g., YouTube, Netflix, Hulu

## Conversational voice/video over IP

VoIP

- interactive nature of human-to-human conversation limits delay tolerance
  e.g., Skype

## Streaming live audio, video

e.g., live sporting event (futbol)

Real-time Transport Protocols: RTP/RTCP/RTSP/SIP

RTP: 运行在UDP 之上，就是封装在UDP包中。

RTP不提供服务质量保证。RTCP来control

## QoS

区分不同的流量类型提供不同等级的服务。

此外，要防止饿死

速率的调节是一种重要的QoS机制。

# lesson2 Internet Applications

DNS

HTTP

CDN

cache