---
layout: post
title:      "Rails-JS Project - Tokidoki Collection"
date:       2020-04-10 00:05:16 +0000
permalink:  rails-js_project_-_tokidoki_collection
---



I decided to build an app called Tokidoki Collection for the Rails-Javascript project.  It uses a Rails API for the back-end of the app.  Javascript, HTML and the Tachyons CSS Design System handle the front-end.

I created seed data to build objects to go in the database.  The app is made up of families of different types of Tokidoki collectible figures.  Each family has many characters and this association is the basis of the project.   The app has the ability to create a Family as well as characters.  The app also has a show page for each family, which renders a characters list for that particular family.

Learning Javascript as someone relatively new to programming was interesting and challenging.  

This app uses the fetch() method to get data from the API back-end for the Family and the Character classes. The  FamilyAPI class uses three fetch methods.  The getFamilyShow class method uses chained .then()s returning JSON serialized objects, courtesy of the Fast JSON API gem.

Here are the Family class API methods.  The getFamilyShow method includes character attributes as each Family has many characters:

class FamilyAPI {
    static getFamilies() {
        return fetch(`${FamilyAPI.base_url}/families`).then(res => res.json())
    }

    static getFamilyShow(familyId) {
        return fetch(`${FamilyAPI.base_url}/families/${familyId}`)
        .then(res => res.json())
            .then(json => { 
                const { 
                    data: { 
                        id,
                        attributes: {
                        name, 
                        photo_url
                    } 
                }, 
                included
            } = json
            return {
                id,
                name,
                photo_url,
                characters: included.map(({id, attributes: {name, description, series, release_year, photo_url, family_id}}) => {
                    return {
                        id,
                        name,
                        description,
                        series,
                        release_year,
                        photo_url,
                        family_id
                    }
                })
            }
        })
    }
		
		static createFamily(familyAttributes) {
        return fetch(`${FamilyAPI.base_url}/families`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'Accept': 'application/json'
            },
            body: JSON.stringify(familyAttributes)
        })
        .then(res => res.json())
    }
}

FamilyAPI.base_url = "http://localhost:3000"



DOM manipulation is handled by the event listeners.

Here is the event listener that handles adding a new character:

if (e.target.matches(".addCharacter")) {
            e.preventDefault()
            let formData = {}
            e.target.querySelectorAll('input[type="text"]').forEach(input => formData[input.id] = input.value)
            formData.family_id = e.target.dataset.family_id
            Character.create(formData)
                .then(character => {
                    document.querySelector('#characters').insertAdjacentHTML('beforeend', character.renderCard())
                })
                    
}

This event listener contains the family_id that the new character will belong to, as the family is the parent class in this app.

This project was the most challenging one yet for me, but I am glad I stuck with it and I hope I can continue learning Javascript as I move forward.  I like the end result of the project very much and hope to expand upon it in the future.
				

