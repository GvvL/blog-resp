---
title: android GestureDetector
date: 2016-06-14 14:18:08
categories: android
tags:
    - android
---
```
public class GestureListenerImpl implements OnGestureListener{
    	@Override
    	public boolean onDown(MotionEvent e) {//触碰时调用
    		return false;
    	}
    
    	@Override
    	public boolean onFling(MotionEvent e1, MotionEvent e2, float velocityX,
    			float velocityY) {//扫动时回调
    		return false;
    	}
    
    	@Override
    	public void onLongPress(MotionEvent e) {//长按时
    	}
    
    	@Override
    	public boolean onScroll(MotionEvent e1, MotionEvent e2, float distanceX,
    			float distanceY) {//滑动时，如果为扫动，则滑动完成时调用
    		return false;
    	}
    
    	@Override
    	public void onShowPress(MotionEvent e) {//按下未移动
    	}
    
    	@Override
    	public boolean onSingleTapUp(MotionEvent e) {//单个手指轻点
    		return false;
    	}

}
```