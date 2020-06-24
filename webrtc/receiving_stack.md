## Decoding

Locations of classes:

```
VideoReceiveStream2: video/video_receive_stream2.cc
VideoReceiver2: modules/video_coding/video_receiver2.cc
VCMGenericDecoder: modules/video_coding/generic_decoder.cc
```



Function calls:

```
VideoReceiveStream2::StartNextDecode() ->
VideoReceiveStream2::HandleEncodedFrame(std::unique_ptr<EncodedFrame> frame) ->
VideoReceiver2::Decode(const VCMEncodedFrame* frame) ->
VCMGenericDecoder::Decode(const VCMEncodedFrame& frame, Timestamp now)
```



`frame_buffer_` is in `VideoReceiveStream2`.



## Rendering

Locations of classes:

```
VCMDecodedFrameCallback: modules/video_coding/generic_decoder.cc
VideoStreamDecoder: video/video_stream_decoder2.cc
IncomeVideoStream: common_video/income_video_stream.cc
VideoRenderFrames: common_video/video_render_frames.cc
```



Function calls:

```
VCMDecodedFrameCallback::Decoded(VideoFrame& decodedImage)
VCMDecodedFrameCallback::Decoded(VideoFrame& decodedImage, int64_t decode_time_ms) -> 
VCMDecodedFrameCallback::Decoded(VideoFrame& decodedImage, absl::optional<int32_t> decode_time_ms, absl::optional<uint8_t> qp) -> 
VideoStreamDecoder::FrameToRender(VideoFrame& video_frame, absl::optional<uint8_t> qp, int32_t decode_time_ms, VideoContentType content_type) ->
IncomingVideoStream::OnFrame(const VideoFrame& video_frame) ->
IncomingVideoStream::Dequeue() ->
absl::optional<VideoFrame> VideoRenderFrames::FrameToRender()
```

