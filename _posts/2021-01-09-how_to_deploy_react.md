---
title: "How to deploy React using Github page?"
excerpt: "Track one's achievement by using the timeline component"
toc: true
toc_sticky: true
published: true
header:
  teaser: /assets/images/2021/01/09/working_example.png
  image: /assets/images/2021/01/09/working_example.png
  caption: "Photo by me"
  og_image: /assets/images/2021/01/09/working_example.png
layout: single
classes: wide

categories:
    - React
tags:
    - React
last_modified_at: 2021-01-09T08:06:00-05:00
---

# Intro 
I saw an interesting post in my favorite community [Dev](https://dev.to/). ["Do you track your achievements?"](https://dev.to/madza/do-you-track-your-achievements-529a) and I visited [Florin Pop's timeline page](https://www.florin-pop.com/timeline). It's a very cool way to track achievements. I think tracking achievements is a great idea. By using the timeline, it's so easy to check out what I'm doing. But, one point to improve the timeline. I can give some effect to the timeline with [React](https://reactjs.org/). Ok, let me bring that into my blog. First, I need to figure out how to deploy React in the [GitHub pages](https://pages.github.com/).

# Procedure
## Required 
I assume that you have a [GitHub](https://github.com/) account. You might be familiar with a command-line interface (terminal or console). In your device, the [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) and [create-react-app](https://www.npmjs.com/package/create-react-app) are installed.  

## Create a repository
There's nothing special about this step. The traditional way to create a repository. We don't need .gitignore, license, and README.md. Frankly, it's up to your decision. To show a working example, I created a test-timeline2 repository. [https://github.com/devjunhong/test-timeline2](https://github.com/devjunhong/test-timeline2)

## Clone
Clone the created repository in your local device using this command.
```sh
$ git clone https://github.com/devjunhong/test-timeline2
```

## Create react app
```sh
$ create-react-app test-timeline2
```
After this, the tool prints "Happy hacking!". By running it, we can check everything works properly. 
```sh
$ cd test-timeline2
$ npm start
```
![react_the_first_example](/assets/images/2021/01/09/react_first_example.png)

If we can see the first example page by create-react-app package like this, it works. 

## Add timeline component
We are going to use a timeline component to create our own. I found [this component](https://www.npmjs.com/package/react-vertical-timeline-component) is applicable in our case. Here is a [demo](https://stephane-monnot.github.io/react-vertical-timeline/#/demo-default-visible) of this component. Looks pretty good. Let's bring the component in our project. We need 2 packages to run it. 
```sh
# current working directory: path/to/test-timeline2 
$ npm i react-vertical-timeline-component
$ npm install @material-ui/icons
```
The 'i' means 'install'. [[1]](#first) Let's update the code. Open the "test-timeline2/src/App.js" and update the code like below. 

```javascript 
{% raw %}
import logo from './logo.svg';
import './App.css';
import { VerticalTimeline, VerticalTimelineElement }  from 'react-vertical-timeline-component';
import 'react-vertical-timeline-component/style.min.css';
import WorkIcon from '@material-ui/icons/Work';
import StarIcon from '@material-ui/icons/Star';

function App() {
  return (
    <div className="App">
      <VerticalTimeline className="vertical-timeline-custom-line">
        <VerticalTimelineElement
          className="vertical-timeline-element--work"
          contentStyle={{ background: 'rgb(33, 150, 243)', color: '#fff' }}
          contentArrowStyle={{ borderRight: '7px solid  rgb(33, 150, 243)' }}
          date="2011 - present"
          iconStyle={{ background: 'rgb(33, 150, 243)', color: '#fff' }}
          icon={<WorkIcon />}
        >
          <h3 className="vertical-timeline-element-title">Creative Director</h3>
          <h4 className="vertical-timeline-element-subtitle">Miami, FL</h4>
          <p>
            Creative Direction, User Experience, Visual Design, Project Management, Team Leading
        </VerticalTimelineElement>

        <VerticalTimelineElement
          iconStyle={{ background: 'rgb(16, 204, 82)', color: '#fff' }}
          icon={<StarIcon />}
        />
      </VerticalTimeline>
    </div>
  );
}

export default App;
{% endraw %}
```

Try to see the result. 
```sh
$ npm start
```
![timeline_missing](/assets/images/2021/01/09/timeline_missing.png)

Do you recognize something strange? As we see in the [demo](https://stephane-monnot.github.io/react-vertical-timeline/#/demo-default-visible), there's one vertical white line and date. In our example, those are missing. Actually, the color of those components are white same as the background color. We can solve this by using two approaches. One is changing the background of the page. Two is to change the color of the line and the date. Here I introduce the second one. 

Let's open "test-timeline2/src/App.css" and add the following in below. 
```css
/* The line */
.vertical-timeline.vertical-timeline-custom-line::before {
  background: #424242;
}

/* date color */
.vertical-timeline-element-date {
  color: black;
}
```
Then, you'll see the line color and date are presented. Nice. 

![timeline_ok](/assets/images/2021/01/09/timeline_ok.png)

## <a name="publish">Publish using Github Page</a>
Ok, we are sure that it runs in the local environment. Next, we are going to publish using the Github Page. And then, going to fill the contents in. 

To publish our work, we need to install one more package.
```sh
$ npm i gh-pages --save-dev
```
The "--save-dev" option will save the package under devDependencies which is useful when installing only development packages that you may not want to ship in production. [[2]](#second)

We need to update "test-timeline2/package.json" file. 
```json 
"homepage": "http://replace_your_github_user_name.github.io/replace_repository_name"
```
The value of the homepage key should be like this. For example, mine is 
```json
"homepage": "https://devjunhong.github.io/test-timeline"
```

One more editing here under the "scripts". We should add two keys("predeploy" and "deploy").
```json
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}
```

Okay. It's time to publish. We need to enter this command.  
```sh
$ npm run deploy 
```
![working_example](/assets/images/2021/01/09/working_example.png)

## Fill the contents in 
To fill the timeline with your story, we need to make copy of code and update the h3, h4 tags like this. Look what I change for content of the h3 tag and the h4 tag. I copied and change "Creative Director" to "UI Designer".

```javascript 
{% raw %}
function App() {
  return (
    <div className="App">
      <VerticalTimeline className="vertical-timeline-custom-line">
        <VerticalTimelineElement
          className="vertical-timeline-element--work"
          contentStyle={{ background: 'rgb(33, 150, 243)', color: '#fff' }}
          contentArrowStyle={{ borderRight: '7px solid  rgb(33, 150, 243)' }}
          date="2011 - present"
          iconStyle={{ background: 'rgb(33, 150, 243)', color: '#fff' }}
          icon={<WorkIcon />}
        >
          <h3 className="vertical-timeline-element-title">Creative Director</h3>
          <h4 className="vertical-timeline-element-subtitle">Miami, FL</h4>
          <p>
            Creative Direction, User Experience, Visual Design, Project Management, Team Leading
        </VerticalTimelineElement>

        <VerticalTimelineElement
          className="vertical-timeline-element--work"
          contentStyle={{ background: 'rgb(33, 150, 243)', color: '#fff' }}
          contentArrowStyle={{ borderRight: '7px solid  rgb(33, 150, 243)' }}
          date="2007 - 2011"
          iconStyle={{ background: 'rgb(33, 150, 243)', color: '#fff' }}
          icon={<WorkIcon />}
        >
          <h3 className="vertical-timeline-element-title">UI Designer</h3>
          <h4 className="vertical-timeline-element-subtitle">Miami, FL</h4>
          <p>
            Design web page, User Experience, Project Management
        </VerticalTimelineElement>

        <VerticalTimelineElement
          iconStyle={{ background: 'rgb(16, 204, 82)', color: '#fff' }}
          icon={<StarIcon />}
        />
      </VerticalTimeline>
    </div>
  );
}
{% endraw %}
```

## Pitfalls 
In the [publishing stage](#publish), I got stuck by 404 error on the GitHub page. I fixed it by changing the repository option. I tried to change the source of branch into master and then back to gh-pages. I see the expected result and the 404 error is gone. 
![github_page_option](/assets/images/2021/01/09/github_page_option.png)


# Outro 
In this post, I didn't update my achievements. Next time, I'm going to update mine and link from this blog to the timeline. If you have a problem or are stuck at some point. Please let me know you can leave a reply by hitting the reaction in the below. Also, you can endorse me to write more. Thank you.

# Reference 
<a name="first">[1]</a> [https://stackoverflow.com/a/49564133/5742992](https://stackoverflow.com/a/49564133/5742992)

<a name="second">[2]</a> [https://stackoverflow.com/a/24739835/5742992](https://stackoverflow.com/a/24739835/5742992)

<a name="third">[3]</a> [https://velog.io/@byjihye/react-github-pages](https://velog.io/@byjihye/react-github-pages)