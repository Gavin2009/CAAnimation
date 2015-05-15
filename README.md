# CAAnimation
show the CoreAnimation
几个可以用来实现热门APP应用PATH中menu效果的几个方法
+(CABasicAnimation *)opacityForever_Animation:(float)time ／／永久闪烁的动画
{
    CABasicAnimation *animation=[CABasicAnimation animationWithKeyPath:@"opacity"];
    animation.fromValue=[NSNumber numberWithFloat:1.0];
    animation.toValue=[NSNumber numberWithFloat:0.0];
    animation.autoreverses=YES;
    animation.duration=time;
    animation.repeatCount=FLT_MAX;
    animation.removedOnCompletion=NO;
    animation.fillMode=kCAFillModeForwards;
    return animation;
}
 
+(CABasicAnimation *)opacityTimes_Animation:(float)repeatTimes durTimes:(float)time; ／／有闪烁次数的动画
{
    CABasicAnimation *animation=[CABasicAnimation animationWithKeyPath:@"opacity"];
    animation.fromValue=[NSNumber numberWithFloat:1.0];
    animation.toValue=[NSNumber numberWithFloat:0.4];
    animation.repeatCount=repeatTimes;
    animation.duration=time;
    animation.removedOnCompletion=NO;
    animation.fillMode=kCAFillModeForwards;
    animation.timingFunction=[CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseIn];
    animation.autoreverses=YES;
    return  animation;
}
 
+(CABasicAnimation *)moveX:(float)time X:(NSNumber *)x ／／横向移动
{
    CABasicAnimation *animation=[CABasicAnimation animationWithKeyPath:@"transform.translation.x"];
    animation.toValue=x;
    animation.duration=time;
    animation.removedOnCompletion=NO;
    animation.fillMode=kCAFillModeForwards;
    return animation;
}
 
+(CABasicAnimation *)moveY:(float)time Y:(NSNumber *)y ／／纵向移动
{
    CABasicAnimation *animation=[CABasicAnimation animationWithKeyPath:@"transform.translation.y"];
    animation.toValue=y;
    animation.duration=time;
    animation.removedOnCompletion=NO;
    animation.fillMode=kCAFillModeForwards;
    return animation;
}
 
+(CABasicAnimation *)scale:(NSNumber *)Multiple orgin:(NSNumber *)orginMultiple durTimes:(float)time Rep:(float)repeatTimes ／／缩放
{
    CABasicAnimation *animation=[CABasicAnimation animationWithKeyPath:@"transform.scale"];
    animation.fromValue=orginMultiple;
    animation.toValue=Multiple;
    animation.duration=time;
    animation.autoreverses=YES;
    animation.repeatCount=repeatTimes;
    animation.removedOnCompletion=NO;
    animation.fillMode=kCAFillModeForwards;
    return animation;
}
 
+(CAAnimationGroup *)groupAnimation:(NSArray *)animationAry durTimes:(float)time Rep:(float)repeatTimes ／／组合动画
{
    CAAnimationGroup *animation=[CAAnimationGroup animation];
    animation.animations=animationAry;
    animation.duration=time;
    animation.repeatCount=repeatTimes;
    animation.removedOnCompletion=NO;
    animation.fillMode=kCAFillModeForwards;
    return animation;
}
 
+(CAKeyframeAnimation *)keyframeAniamtion:(CGMutablePathRef)path durTimes:(float)time Rep:(float)repeatTimes ／／路径动画
{
    CAKeyframeAnimation *animation=[CAKeyframeAnimation animationWithKeyPath:@"position"];
    animation.path=path;
    animation.removedOnCompletion=NO;
    animation.fillMode=kCAFillModeForwards;
    animation.timingFunction=[CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseIn];
    animation.autoreverses=NO;
    animation.duration=time;
    animation.repeatCount=repeatTimes;
    return animation;
}
 
+(CABasicAnimation *)movepoint:(CGPoint )point ／／点移动
{
    CABasicAnimation *animation=[CABasicAnimation animationWithKeyPath:@"transform.translation"];
    animation.toValue=[NSValue valueWithCGPoint:point];
    animation.removedOnCompletion=NO;
    animation.fillMode=kCAFillModeForwards;
    return animation;
}
 
+(CABasicAnimation *)rotation:(float)dur degree:(float)degree direction:(int)direction repeatCount:(int)repeatCount ／／旋转
{
    CATransform3D rotationTransform  = CATransform3DMakeRotation(degree, 0, 0,direction);
    CABasicAnimation* animation;
    animation = [CABasicAnimation animationWithKeyPath:@"transform"];
 
animation.toValue= [NSValue valueWithCATransform3D:rotationTransform];
    animation.duration= dur;
animation.autoreverses= NO;
    animation.cumulative= YES;
    animation.removedOnCompletion=NO;
    animation.fillMode=kCAFillModeForwards;
    animation.repeatCount= repeatCount; 
animation.delegate= self;
 
return animation;
}


- (void)viewDidLoad {

    [super viewDidLoad];


layer=[CALayer layer];

layer.frame=CGRectMake(50, 200, 50, 50);

layer.backgroundColor=[UIColor orangeColor].CGColor;

layer.cornerRadius=8.0f;


CABasicAnimation *animation=[CABasicAnimation animationWithKeyPath:@"transform.translation.y"];

animation.duration=4.0f;

animation.autoreverses=NO;

animation.repeatCount=1;

animation.toValue=[NSNumber numberWithInt:-10];

animation.fromValue=[NSNumber numberWithInt:200];

animation.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseInEaseOut];


CABasicAnimation *animationZoomIn=[CABasicAnimation animationWithKeyPath:@"transform.scale"];

animationZoomIn.duration=2.0f;

animationZoomIn.autoreverses=NO;

animationZoomIn.repeatCount=1;

animationZoomIn.toValue=[NSNumber numberWithFloat:1.56];

animationZoomIn.timingFunction=[CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseIn];

CABasicAnimation *animationZoomOut=[CABasicAnimation animationWithKeyPath:@"transform.scale"];

animationZoomOut.beginTime=2.0f;

animationZoomOut.duration=2.0f;

animationZoomOut.autoreverses=NO;

animationZoomOut.repeatCount=1;

animationZoomOut.toValue=[NSNumber numberWithFloat:.01];

animationZoomOut.timingFunction=[CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseOut];

CAAnimationGroup *group=[CAAnimationGroup animation];

group.duration=4.0f;

group.animations=[NSArray arrayWithObjects: animation, animationZoomIn, animationZoomOut,nil];

group.removedOnCompletion=NO;

group.fillMode=kCAFillModeForwards;

[layer addAnimation:group forKey:nil];

[self.view.layer addSublayer:layer];

CABasicAnimation *pulse = [CABasicAnimation animationWithKeyPath:@"transform.scale"];
    pulse.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseOut];
    pulse.duration = 0.5 + (rand() % 10) * 0.05;
    pulse.repeatCount = 1;
    pulse.autoreverses = YES;
    pulse.fromValue = [NSNumber numberWithFloat:.8];
    pulse.toValue = [NSNumber numberWithFloat:1.2];
    [self.ui_View.layer addAnimation:pulse forKey:nil];

// bounds
 
CABasicAnimation *anim = [CABasicAnimation animationWithKeyPath:@"bounds"];
    anim.duration = 1.f;
    anim.fromValue = [NSValue valueWithCGRect:CGRectMake(0,0,10,10)];
    anim.toValue = [NSValue valueWithCGRect:CGRectMake(10,10,200,200)];
    anim.byValue  = [NSValue valueWithCGRect:self. ui_View.bounds]; 
//    anim.toValue = (id)[UIColor redColor].CGColor;
//    anim.fromValue =  (id)[UIColor blackColor].CGColor;
    
    anim.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseInEaseOut];
    anim.repeatCount = 1;
    anim.autoreverses = YES;
    
    [ui_View.layer addAnimation:anim forKey:nil];
//cornerRadius
 
    CABasicAnimation *anim2 = [CABasicAnimation animationWithKeyPath:@"cornerRadius"];
    anim2.duration = 1.f;
    anim2.fromValue = [NSNumber numberWithFloat:0.f];
    anim2.toValue = [NSNumber numberWithFloat:20.f];
    anim2.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseInEaseOut];
    anim2.repeatCount = CGFLOAT_MAX;
    anim2.autoreverses = YES;
    
    [ui_View.layer addAnimation:anim2 forKey:@"cornerRadius"];

//contents
 
CABasicAnimation *anim = [CABasicAnimation animationWithKeyPath:@"contents"];
    anim.duration = 1.f;
    anim.fromValue = (id)[UIImage imageNamed:@"1.jpg"].CGImage;
    anim.toValue = (id)[UIImage imageNamed:@"2.png"].CGImage;
//    anim.byValue  = (id)[UIImage imageNamed:@"3.png"].CGImage;
//    anim.toValue = (id)[UIColor redColor].CGColor;
//    anim.fromValue =  (id)[UIColor blackColor].CGColor;
    
    anim.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseInEaseOut];
    anim.repeatCount = CGFLOAT_MAX;
    anim.autoreverses = YES;
    
    [ui_View.layer addAnimation:anim forKey:nil];


 
[ui_View.layer setShadowOffset:CGSizeMake(2,2)];
    [ui_View.layer setShadowOpacity:1];
    [ui_View.layer setShadowColor:[UIColor grayColor].CGColor];
//
    CABasicAnimation *anim = [CABasicAnimation animationWithKeyPath:@"shadowColor"];
    anim.duration = 1.f;
    anim.toValue = (id)[UIColor redColor].CGColor;
    anim.fromValue =  (id)[UIColor blackColor].CGColor;
    
    anim.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseInEaseOut];
    anim.repeatCount = CGFLOAT_MAX;
    anim.autoreverses = YES;
    
    [ui_View.layer addAnimation:anim forKey:nil];
    
    CABasicAnimation *_anim = [CABasicAnimation animationWithKeyPath:@"shadowOffset"];
    _anim.duration = 1.f;
    _anim.fromValue = [NSValue valueWithCGSize:CGSizeMake(0,0)];
    _anim.toValue = [NSValue valueWithCGSize:CGSizeMake(3,3)];
    
    _anim.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseInEaseOut];
    _anim.repeatCount = CGFLOAT_MAX;
    _anim.autoreverses = YES;
    
    [ui_View.layer addAnimation:_anim forKey:nil];
    
    
    CABasicAnimation *_anim1 = [CABasicAnimation animationWithKeyPath:@"shadowOpacity"];
    _anim1.duration = 1.f;
    _anim1.fromValue = [NSNumber numberWithFloat:0.5];
    _anim1.toValue = [NSNumber numberWithFloat:1];
    
    _anim1.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseInEaseOut];
    _anim1.repeatCount = CGFLOAT_MAX;
    _anim1.autoreverses = YES;
    
    [ui_View.layer addAnimation:_anim1 forKey:nil];
    
    
    
    CABasicAnimation *_anim2 = [CABasicAnimation animationWithKeyPath:@"shadowRadius"];
    _anim2.duration = 1.f;
    _anim2.fromValue = [NSNumber numberWithFloat:10];
    _anim2.toValue = [NSNumber numberWithFloat:5];
    
    _anim2.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseInEaseOut];
    _anim2.repeatCount = CGFLOAT_MAX;
    _anim2.autoreverses = YES;
    
    [ui_View.layer addAnimation:_anim2 forKey:nil];

//layer.hidden=YES;

}
