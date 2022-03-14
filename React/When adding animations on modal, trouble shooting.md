```
<Trouble shooting>
1-1. problem: component rerendered but animation didn't work.
   I thought that (parent's some state didn't change) or (state changed but didn't pass to child component) or (state passed to child but the component didn't rerender,) etc...
   I tested all, and found that everything is okay except animation when component rerendered.
1-2. to solve: putting "key" is the key to solve the problem!
   I got this from
   (stack overflow Q&A : https://stackoverflow.com/questions/63186710/how-to-trigger-a-css-animation-on-every-time-a-react-component-re-renders)
     answer1 : "when the div re-renders, react only changes its inner text. Adding a key will make react think it's a different div when the key changes, so it'll unmount it and mount again."
     answer2 : "The trick here is to use a random key field on your card element. React's diffing algorithm considers elements with the same key as the same, so randomizing the key will make react consider each rerendered element as new, so will removed the old element from the DOM and add a brand new one"
But I had second problem.(What?????????)
2-1. problem: when boolean prop is false, animation for prop true works...
     I have two animations. One is for true, the other is for false.
     In one styled-component, boolean prop works for dividing animations.
     But always animation for true works, animation for false never.
     They were not problem that styled-component prop type or ThemProvider or React.memo or component key prop, etc...
     Huh...I couldn't catch the main reason. But I solved it.
2-2. to solve: two components, two animations. not one component, two animations
     before I solved it, I had one component, and boolean prop divided animations.
     Now I have two components, which have another animation.
     And boolean prop decides which component will be returned.
3-3. At last, things are unnecessary : key prop and boolean prop for styled-components.
     Bye guys...
```
     
![20220315_01](https://user-images.githubusercontent.com/60069112/158220440-c9ad76e6-4a16-402c-8d2e-c82563fb42c5.png)
![20220315_02](https://user-images.githubusercontent.com/60069112/158220461-586780d6-36c2-47d2-8b5b-9d43502f4c84.png)   
Finally--------------------  
![20220315_06](https://user-images.githubusercontent.com/60069112/158222227-c5787942-6857-42df-af26-f19115aa220b.png)

https://user-images.githubusercontent.com/60069112/158222525-2836fc38-882d-442b-876c-46ea61838140.mp4

```Oops I found another problem.  After scrolling in modal, clicking the closing button, then top place in modal is showed.
Yeah... got it... I returned to problem 2... haha...
now time is over 2 am. I go asleep...
```
