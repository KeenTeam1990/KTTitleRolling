# CDDTitleRolling
电商轮播标题广告（仿京东、淘宝）
![项目效果图](https://github.com/KeenTeam1990/KTTitleRolling/blob/master/CDDTitleRolling/pic/55.gif) 

![项目结构图](https://github.com/KeenTeam1990/KTTitleRolling/blob/master/CDDTitleRolling/pic/11.jpg "效果图")

实现方面，我利用UIView animateWithDuration结合CALayer的CATransform3D坐标变换做上下翻滚动画。

#pragma mark - 标题滚动
- (void)titleRolling{
    
    if (self.saveMiddleArray.count > 1) { //所存的每组滚动
        __weak typeof(self)weakSelf = self;
        
        [UIView animateWithDuration:self.rollingTime animations:^{
            
            [self getMiddleArrayWithIndex:0 WithAngle:- M_PI_2 Height:- RollingViewHeight / 2]; //第0组
            
            [self getMiddleArrayWithIndex:1 WithAngle:0 Height:0]; //第一组
            
        } completion:^(BOOL finished) {
            
            if (finished == YES) { //旋转结束
                UIButton *newMiddleView = [weakSelf getMiddleArrayWithIndex:0 WithAngle:M_PI_2 Height: -RollingViewHeight / 2];
                [weakSelf.saveMiddleArray addObject:newMiddleView];
                
                [weakSelf.saveMiddleArray removeObjectAtIndex:0];
            }
        }];
    }
    
}

#pragma mark - CATransform3D翻转
- (UIButton *)getMiddleArrayWithIndex:(NSInteger)index WithAngle:(CGFloat)angle Height:(CGFloat)height
{
    if (index > _saveMiddleArray.count) return 0;
    UIButton *middleView = self.saveMiddleArray[index];
    
    CATransform3D trans = CATransform3DIdentity;
    trans = CATransform3DMakeRotation(angle, 1, 0, 0);
    trans = CATransform3DTranslate(trans, 0, height, height);
    middleView.layer.transform = trans;
    
    return middleView;
}


如果这个Demo让你有所收获，请Star and Fork。

注：如果遇到问题还请Issues,我会尽快回复。



