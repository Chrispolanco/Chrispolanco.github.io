---
layout: post
title:      "Arrow function and “this”, like peanut butter and jelly "
date:       2020-07-07 05:25:58 +0000
permalink:  arrow_function_and_this_like_peanut_butter_and_jelly
---


After delving into a plethora of guides and youtube videos, to gain a greater understanding of how the arrow function and “this” work in conjunction as well as separately. I’ve come to the conclusion that I joined the same club as many other developers that have come before me. That cost to join this exclusive club is the struggle and frustration in trying to understand both functions' nuances. This is a club that I am proud to be in. It is the first step in a  journey in truly trying to mold and create javascript projects that really show what javascript is capable of. 

Through this struggle I have gained a greater insight into how the arrow function and “this” work, both independently as well as in conjunction with one another. That being stated, I still have many more projects to build before I can say with any confidence that I have grasped both methods. Given that my project’s foundation was based on utilizing both a great extent the first steps have been taken. Albeit a few missteps did occur along the way. Honestly a lot of missteps happened but the important thing is that growth occurred. 

My project relies heavily on ensuring that information is properly transferred from one function to the next. Any break and my whole application comes crashing down. Which it did on multiple occasions. Below I have included an example on the importance of using “bind” with “this”. 

`        
this.menu_choice_one.addEventListener('click', this.userSignUp.bind(this));
` 

Explanation of the above code. Once the element titled this.menu_choice_one, it’s a button, is clicked it will result in the method userSignUp being executed. As a side note one important thing to note is if a function includes () alone it will be called upon as soon as the code runs. For that reason it is prudent that it not be included if the action is to run as a result of an action. Such as the example above with a click. In this example the action bind(this) will not be executed right away since it is together. 

One important thing to note is the reason that bind(this) is required is if it is not used the error that populates is as follows: 

`
this.menu_choice_one.addEventListener('click', this.userSignUp);
`

Results in: 

`
Uncaught TypeError: Cannot assign to read only property 'form' of object '#<HTMLButtonElement>'
`

The reason this populates is that instead of User.userSignup being executed the function is being called on the `<HTMLButtonElement>`. In order to remedy this solution I use bind(this) which results in the User being binded to this action instead of the element that called the function. 

Another detail to note from this function is the this.userSignUp portion of the function. The reason that this is required twice is that if the first `this` is not included it will attempt to call the function on this.menu_choice_one which will result in the following error: 

` 
users.js:166 Uncaught ReferenceError: userSignUp is not defined
    at Users.menuChoice
`

In this situation the function is attempting to be found within the Users.menuChoice which it does not find. By adding this to the start of the function alongside bind(this) Users is reached where the function will be found and be properly executed. 

The power of the arrow function alongside `this` can be seen below. 


 
        this.wrapper_questions.addEventListener('click', (e)=> {
            e.preventDefault(); 
            if(e.target.innerText === this.adventureInfo.answer_1) {
                this.correctChoiceOne(); 
            } else if (e.target.innerText !== this.adventureInfo.answer_1 && this.hero.health > 0) { 
            this.wrongChoiceOne() 
            this.hero.health = 0 
            } else { 
                this.loss();
            }; 
        })

The arrow function utilizes Lexical Scoping. Which signifies that the value of “this” is always inherited from the enclosing scope. That is the reason that for this function “bind(this)” was not required in order to call the function correctChoiceOne, wrongChoiceOne, or loss. While one `this` is still required to call the function two are not required as they are in a regular function. 

