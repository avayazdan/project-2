# PROJECT 2 - DUNGEONS & DRAGONS CHARACTER BUILDER

Deployed at: https://dndgeneratorr.netlify.app/

This project was built for project two of General Assembly's Full-Stack Software Engineering course. 
The project brief's focus was on utilising our knowledge of React as well as fetching and using data from selected API's. 
This project is a paired project. Made with total nerdy love by Claudia and Ava. The timeframe for this project was one week.


### Table of contents 

1. How it works
2. Planning 
3. Build
4. Styling
5. Challenges and Wins
6. Future improvements

#### How it works

The Dungeons & Dragons Character Builder is a generator that fetches random data from an API and displays it to the user. The random data returned is race, class and skill.
It also fetches the description of the randomised data if the user wishes to see it. (Description of returned race, class and skill, including the languages spoken by the race and their ageing attributes)
The purpose of the generator is for players’ to have a random character generated for them to play the game.
The players’ can randomise their character as many times as they wish. 

#### Planning

We were given the task to find and play around with a list of available API's and others we could find online. 
We first tested the API's using Insomnia and the D&D API documentation (https://www.dnd5eapi.co/).
Once we agreed on what the project would do and display, we started to experiment with creating wireframes.

![planning screenshot](/src/assets/psuedo.png)

We also kept track of the things we had to do for each day. We stayed in touch via Slack and set up personal Zoom meetings to discuss things outside of class time if necessary. We used a Trello board to keep track of the things we had to do. At first, we began by working on the project together via Zoom, however as we only had one week, we decided to split the tasks between us. After day 3, we decided to split the styling (Ava) and logic (Claudia) between us, still helping each other whenever we got stuck on things along the way.

![planning screenshot](/src/assets/psuedo2.png)

#### Build

The project utilises React, HTML and SCSS. We started by testing the API's behaviour using <font color="blue">**console.logs**</font> and using the 
terminal in the Chrome browser to see how we could access different data points. Then we fetched the data within our code.

```
async function fetchClassInfo(randomClass) {
    const respFour = await fetch(`https://www.dnd5eapi.co/api/classes/${randomClass.index}`)
    const classInfo = await respFour.json()
    updateClassInfo(classInfo)
    displayClassInfoFunction(classInfo)
    hitDieDisplay(classInfo)
  }
  //fetching individual race information
  async function fetchRaceInfo(randomRace) {
    const respFive = await fetch(`https://www.dnd5eapi.co/api/races/${randomRace.index}`)
    const raceInfo = await respFive.json()
    updateRaceInfo(raceInfo)
  }
  async function fetchSkillInfo(randomSkill) {
    const respSix = await fetch(`https://www.dnd5eapi.co/api/skills/${randomSkill.index}`)
    const skillInfo = await respSix.json()
    updateSkillInfo(skillInfo)
  }
```

Our next step was to be able to return a random character, which we tackled by using the <font color="blue">**Math.random()**</font> function. 

```
  function generateCharacter() {
    randomClass = classes.results[Math.floor(Math.random() * classes.results.length)]
    fetchClassInfo(randomClass)
    displayingClassImg(randomClass)
    updateRandomClass(randomClass)

    randomRace = races.results[Math.floor(Math.random() * races.results.length)]
    fetchRaceInfo(randomRace)
    updateRandomRace(randomRace)

    randomSkill = skills.results[Math.floor(Math.random() * skills.results.length)]
    fetchSkillInfo(randomSkill)
    updateRandomSkill(randomSkill)
  }
  }
```

The main logic in this project is within our generator which is the code we expanded above.  

#### Styling

We wanted the styling to reflect classic D&D characteristics and aesthetics but still have a modern feel. 
We added extra styling functionality like hover effects to give the project more character. 
We used different art styles such as AI created digital art as well as classic drawings.
We also used classic D&D iconography such as the D20 infamous dice. 

I wanted to include famous iconography from D&D, I also wanted there to be a feel of consistently throughout, luckily I was able to find sets of D&D art by the same artists, and was able to find art sets which made certain sections consistent. I also found a D&D font, which I was able to import and utilise in our project. 

![planning screenshot](/src/assets/stylescreen.png)
![dice](/src/assets/dice3.png)

Below, the SCSS for the button I designed and the corresponding HTML. The dice is fit inside a flex container to act as the center point of the button, the hover cursor changes to indicate it as a clickable element, and I added hover effects to the button:after to add some finishing touches. 

```
      <div className="button-container">
        <div className="button-border">
          <h3>Click below to Generate a character</h3>
          <div className="button-1-container">
            <button className="button-1" onClick={generateCharacter}>
              <img className="dice" src={diceImg} />
            </button>
          </div>

.button-container {
  display: flex;
  justify-content: center;
}

.dice {
  width: 55px;
  height: 55px;
}

.button-1 {
  font-size: 25px;
  font-weight: 200;
  letter-spacing: 1px;
  padding: 13px 50px 13px;
  margin-bottom: 60px;
  outline: 0;
  border: 2px solid black;
  cursor: pointer;
  font-family: buttonFont;
  display: flex;
  height: 110px;
  width: 170px;
  justify-content: flex-end;
  flex-direction: column;
  flex-wrap: nowrap;
  align-items: center;
}

.button-1::after {
  content: "";
  background-color: #9d0a0e !important;
  width: 100% !important;
  z-index: -1 !important;
  position: absolute !important;
  height: 100% !important;
  top: 7px !important;
  left: 7px !important;
  transition: 0.2s !important;
}

.button-1:hover::after {
  top: 0px !important;
  left: 0px !important;
}

.button-border {
  border: 3px solid #333333;
  border-radius: 2% 6% 5% 4% / 1% 1% 2% 4%;
  border-width: 5px;
  width: 600px;
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-image: url(../assets/nav.png);
  opacity: 0.9;
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.button-border::hover {
  opacity: 1;
}

```


#### Challenges and Wins

A few challenges appeared during the building of this project. But with every challenge there was a win. The biggest challenge was getting the favourites functionality to work. We discovered that there are many ways to do it and the simplest way would come with a lot of caveats, such as losing the data from each page when clicked onto a new page. The biggest challenge that we faced was during the deployment stage, we discovered that we had to fix a number of syntax issues for it to be successfully deployed online, that we would not have known until the deployment stage. We had many wins, such as figuring out the little nuances of the D&D API, as it was quite complex - there was a lot of data nested within different objects and it was hard to retrieve certain parts of the data at first. Once we understood exactly how the objects worked it was easy to use and understand, and this was definitely a win. 

#### Future improvements 

Originally we had planned to have a Favourites page for the user's to save up to four characters. (4 character's plus the Dungeon Master). Another option would be to have an infinite amount of favourites for the player's to potentially round up their favourite generated character's and choose. The addition of favourites would have been a relevant feature to our project as it would emphasise the concept of generating a character for the user to potentially play with in a campaign. The player's would be able to see their favourite's in the favourite's page as well as which user saved it to favourites.. We would also have the option to expand details of the class, race and skills so that it is not lost in the home-page. 
In terms of styling, having the expansions more concise and in clear sections would be the finishing touch. 


#### Key learnings / Main takeaways

This was the first time I had worked with another person on a project, and so the value and key takeaways from this project was learning about collaboration, planning, communication and so on. I learnt that I enjoy working with others and how working in a team can hold so much value when programming or web designing. My partner gave me insights to styling ideas that I may have overlooked, and likewise I helped her with programming problems she may have been stuck on or needed help with. It was nice to work on two separate components but at the same time give input and make changes in each others work with each others consent when need be. I also enjoyed discussing ideas and methods.
