---
layout: post
title:      "My First JavaScript Application"
date:       2021-04-11 19:17:11 -0400
permalink:  my_first_javascript_application
---

I recently built my first web application using JavaScript for Flatiron School. Having never touched JavaScript and hearing how hard it is to learn made me nervous when it was time to start module 4. For this application, I used Rails API backend and JavaScript for my front end which utilized classes and asynchronously handled all interactions between backend and frontend.

The app I designed is a flashcard application that displays deck names of all the modules I have completed so far at Flatiron School and others I want to start learning (Ruby, Rails, JavaScript, Data Structures, and Algorithms). I had a really hard time deciding what to build, so I decided to build an application for something that I do often: write flashcards.

**The Backend**

![](https://miro.medium.com/max/4800/1*v-sqGV8FAYKK1XAPVy1aoQ.png)

**Frontend Structure**

![](https://miro.medium.com/max/1132/1*JN2qs5u4cQGF-r7aDD4QDA.png)

For the frontend I decided to create multiple files all having a single responsibility, it helped me a lot when debugging and trying to locate errors.
The most challenging part of this project was the PATCH request for my Card model, there were many steps and I found myself lost on how to even begin. So I will break it down to have as a reference for myself in the future or to help anyone who may be stuck.

**Step #1 Listen for the event to happen**

In this case listen for two events, when the edit button gets clicked to display the edit form and the submit event when the save button gets clicked
```
#edit button
if (e.target.classList.contains("editBtn")) {
			console.log("edit button clicked")
      this.createEditFields(e.target);
}
#Save button
this.card.addEventListener("submit", this.submitEditForm);
submitEditForm = (e) => {
    e.preventDefault();
    console.log("edit form save button clicked")
    const cardId = e.target.dataset.id;
    cardApi.patchCard(cardId);
  };
```

I decided to attach my event listener to the card as soon as it gets attached to the DOM. The card had no other submit event or form to listen so it would only handle the edit form submission.

**Step #2 Replace the card div with form div which will display the fields to edit.**

I am leveraging off the event passed in by the handleClick method which was the edit button.
Now we just need to attach the form text area fields that will display the current innerText of the card that got clicked on. To populate the text area fields we get the element that is triggering the event. I used editBtn.contains(“.card”) to traverse the DOM and find the parent of that button.
```
createEditFields = (editBtn) => {
    const card = editBtn.closest(".card");
    const front = card.querySelector(".cardFront h2").innerText;
    const back = card.querySelector(".cardBack p").innerText;
    this.card.innerHTML = `
    <form class="update-form" data-id="${this.id}">
    <label for="front">Question</label>
    <textarea name="front" class="update-front-${this.id}" value="${front}">${front}</textarea>
    <label for="back">Answer</label>
    <textarea name="back" class="update-back-${this.id}" value="${back}">${back}</textarea>
    <input type="submit" name="submit" value="SAVE" class="saveBtn" data-id="${this.id}">
    <form>
    `;
  };
```

**Step #3 Select Inputs**

These inputs are what we will save in our server and will also need to display the values of on our front end.
```
# Card Patch
const front = document.querySelector(`.update-front-${cardId}`).value;
const back = document.querySelector(`.update-back-${cardId}`).value;
```

**Step #4 Patch Request**

This is where we need to save information to our database. In our PATCH request, take our selected input from our edit form and include that data in the body of the HTTP message. (The data will need to be converted back into a string).

```
let cardObj = {
      front: front,
      back: back,
    };
body: JSON.stringify(cardObj),
```

**Step #5 Add to DOM!**

Once the server-side is taken care of, we need to display these changes in the DOM. First, we need to use .json() once we get the response body back from our promise so that it’s in a format that our front end can easily understand. Since we are updating an already existing card and not creating a new one, we have to find the ID and render that card with the data that we received from our second promise. However, we need to unpack this data by using the destructuring assignment which will provide a cleaner and neater way to extract data from our objects.

```
#destructuring
renderUpdatedCard = ({ front, back }) => {
    this.front = front;
    this.back = back;
    this.renderHTML();
  };
#after promise
let findCard = Card.findById(card.data.id);
findCard.renderUpdatedCard(card.data.attributes);
```

Although a small application, I felt super accomplished once I got it working. With 6 weeks of JavaScript under my belt, this is only the beginning. I am nowhere near where I’d like to be with my JavaScript knowledge, there is still so much to learn!!!

[A great resource that really helped me understand fetch requests and promises: ](https://www.youtube.com/user/shiffman)

[A great playlist that helps explain how code is executed under the hood in Javascript: ](https://www.youtube.com/playlist?list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP)

Short Demo:

![](https://miro.medium.com/max/1400/1*uYiMOuDs5NfVDS4Zw2x4ww.gif)

