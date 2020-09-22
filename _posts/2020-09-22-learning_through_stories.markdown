---
layout: post
title:      "Learning through stories"
date:       2020-09-22 05:54:09 +0000
permalink:  learning_through_stories
---


You make plans and god laughs. It’s a saying that has been around for such a long time and yet to this day people including myself still continue to make plans. Sufficient to say for this last React project there was plenty of laughing. I started this last project with the intention of making a site that resembled instagram. Where local astronomers would be able to to upload photos they took with their telescopes and put in on the website. The local astronomers would be able to write a little snippet description, the coordinates of when they took it and have the ability for other users of the site to be able to write comments about the uploaded photos. I was also planning on brining in other API's as well. Unfortunately due to becoming ill, I was not able to spend the time I had originally planned on the application. This led me to change the application around to a great deal. 

One of the main factors I decided to leave for a future project was the ability for users to upload their own images. Which led to a redesign for what the application would be used for. During my thought process I remembered in my childhood how in my culture we have stories that are unique, that are not widely known. Which led me to think about how an application which allowed users to type down stories from their cultures could be entertaining and lead to greater understanding. 

One feature that at the start of the project I didn’t give much thought to but toward the end I realized just how important it was, was the ability to to change from one component to another when an action is completed. The ability for when a user signs in or logouts to bw taken to the component/container of my selection. After some research I found the answer to the problem and it was history.push(). With history.push() I was able to send the user to the location of selection after an action was undertaken. In the example below after a user signs out I use history.push(‘/login’) the user is sent to the login component. 

```
import React from 'react'; 
import { connect } from 'react-redux'; 
import { logout } from '../../actions/user'; 

const Logout = ({ logout, history }) => {
    return (
        <form onSubmit={(event) => { 
            event.preventDefault()
            logout()
            history.push('/login')
        }
    }>
            <button type="submit" className="button">Log Out</button>
        </form>
    )
}

export default connect(null, {logout})(Logout)
```
 
Simple, after believing that was all I needed to known I tried the same solution on my PostForm component and was greeted with the following error:

**TypeError: Cannot read property 'push' of undefined**


PostForm Container

```
import React, { Component } from 'react';
import { connect } from 'react-redux'; 
import { createPost } from '../../actions/posts'; 
import { withRouter } from 'react-router-dom'; 


class PostForm extends Component {

    constructor(props){
        super(props); 
        this.state = {
            location: '', 
            story: '', 
            user_id: this.props.userLoggedIn.id
        }
    }

    handleOnChange = (event) => {
        this.setState({
            [event.target.name]: event.target.value 
        })
    }

    handleOnSubmit = (event) => {
        event.preventDefault(); 
        this.props.createPost(this.state)
        this.setState({
            location: '', 
            story: ''
        })
        this.props.history.push('/personalPosts')
    }

    render() {
        return(
            <div className="container"> 
                <form className="form" onSubmit={this.handleOnSubmit}> 
                    <label htmlFor="location" className="InnerForm">Location</label>
                    <input type="text" name="location" onChange={this.handleOnChange} value={this.state.location}/> 
                    <label htmlFor="story" className="InnerForm">Story</label>
                    <textarea type="text" name="story" onChange={this.handleOnChange}  value={this.state.story}/> 
                <button type="submit" className="StoryButton">Submit Story</button>
                </form>
            </div>
        )
    }

}

export default withRouter(connect(null, { createPost })(PostForm))
```

I didn’t understand the reason for the error so I went back to Stackoverflow and blogs on medium and other sources to try to garner a better understanding as to the reason it was not working. It is then when I learned more about React Router. 

The basics of React Router:

When a component is rendered by React Router it passes three props to that component: location, match, and history. With history, history.push() becomes available to be used within the component, which is what allows the redirecting to another route. In my application Logout is rendered through React Router which allowed history to be used. 

Fixing PostForm: 

The first steps was importing “withRouter” from “react-router-dom” onto my PostFrom container. Then adding “withRouter” when exporting this section: 

```
export default withRouter(connect(null, { createPost })(PostForm))
```

By doing so this section had access to through props to the history feature, allowing the user to be rerouted after the form is submitted. Easy pesy just took a little more understanding. 

While this project definitely changed from was originally planned the framework that I built can be used for my original idea. With time I will be building out my original idea since I already have a vision for how I want it to look. The features I want it to have and so much more. I learned so much from this final project as well. Which is going to make building out my idea so much easier as well. In addition that framework can be used for many other ideas. So I’ll be having the last laugh on this one.

