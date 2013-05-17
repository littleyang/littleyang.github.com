---
uri: /cs/program/java/pattern/observer
permalink: /cs/program/java/pattern/observer/index.html
layout: post
title: "java观察者模式"
description: ""
category:
tags: []
---
{% include JB/setup %}

### 什么是观察者模式？

先看图，再来解释一下:

![Imgur](http://i.imgur.com/CZnnBNs.png)

ok,先来看看下面这段话:

>
>The intent of the OBSERVER pattern is to define a one-to-many
dependency between objects so that when one object changes
state, all its dependents are notified so that they can react to the
change.
>

观察者的目的就是建立一个一对多的相互独立的关系，当一个对象的状态发生变化的时候，所有对应的观察者都会接到变化的通知XX已经
改变了，你们的状态也要改变，以便客户端知道啊！不要偷懒，很简单吧！

这种模式呢，很多时候都是用在GUI里面的，比如说监听鼠标事件，点击按钮事件等！其他方面也用的有的。这个就是观察者模式


### 直接上个代码

```java

/**
 * the observer pattern:
 *  A certain object observed by other object(Observer). when the subject object'status
 *  changes,notify all observers and they change own status that is respondent to subject
 *  maybe there are many observer so,the subject should has an array to store the observers
 *
 * @author jenny
 *
 */
public abstract class AbsSubject {

     // an array to store the observer
     private List<InterfObserver> observerList = new ArrayList<InterfObserver>();

     /*
      * 添加观察者对象
      */
     public void addObserver(InterfObserver observer){
         // add observer
         observerList.add(observer);
     }

     /*
      * remove observer
      */
     public void removeObserver(InterfObserver observer){
         observerList.remove(observer);
     }

      /*
       * notify all observers
       */
     public void notifyAllObservers(String state){

           for(InterfObserver observer : observerList){
                observer.updateStatus(state);
           }
    }


/**
 * this is the certain observed object
 * @author jenny
 *
 */
public class ConcrentSubject extends AbsSubject {

     // define the object status
     private String status;

     public String getStatus() {
         return status;
     }

     public void setStatus(String status) {
         this.status = status;
     }

     /*
      * change the status and notify all observer
      */
     public void changeAndNotify(String newStatus){
         status = newStatus;
         System.out.println("new status is: "+ status);
         this.notifyAllObservers(status);
     }

}


/**
 * this is the observer interface and contain a method that update the observer status
 * @author jenny
 *
 */
public interface InterfObserver {

    public void updateStatus(String state);

}



/**
 * this is the concrete observer object
 * @author jenny
 *
 */
public class ConcrentObserver implements InterfObserver {

    // define the observer's status
    private String observerStatus;

    @Override
    public void updateStatus(String state) {
         // TODO Auto-generated method stub
         // update the observer's status
         setObserverStatus(state);
         System.out.println("Observer status is: "+observerStatus);
    }

    public String getObserverStatus() {
          return observerStatus;
    }

    public void setObserverStatus(String observerStatus) {
         this.observerStatus = observerStatus;
    }

}



/**
 * this is the client class
 * @author jenny
 *
 */
public class MainTest {

   public static void main(String[] args){

       // create the concrete subject
       ConcrentSubject cs = new ConcrentSubject();
       // create the concrete observer
       ConcrentObserver co = new ConcrentObserver();

       cs.addObserver(co);
       cs.changeAndNotify("New status");
    }
}

```



