# ijkmediaframework_bitcode
1、support bitcode
2、support armv7 x86_64 arm64
3、auto rotation

```
File: IJKFFMoviePlayerController.m
- (void)postEvent: (IJKFFMoviePlayerMessage *)msg {
    ...
    case FFP_MSG_VIDEO_ROTATION_CHANGED: {
        int degree = avmsg->arg1;
        NSLog(@"FFP_MSG_VIDEO_ROTATION_CHANGED: %d°\n", degree);
        if (_autoRotationVideo) {
            CGRect frame = _glView.frame;
            _glView.transform = CGAffineTransformMakeRotation(degree * M_PI / 180);
            _glView.frame = frame;
        }

        [[NSNotificationCenter defaultCenter]
         postNotificationName:IJKMPMoviePlayerRotationChangedNotification
         object:self userInfo:@{IJKMPMoviePlayerRotationDegreeKey : @(avmsg->arg1), IJKMPMoviePlayerVideoUrlString : _urlString}];
        break;
    }
    ...
}
```
