---
layout: page
title: Where Should We Eat in the Boise Area?
description: >-
  A one-button random picker that draws from our full list of favorite
  Boise-area restaurants — for nights when nobody can decide where to eat.
permalink: /where-should-we-eat/
comments: true
---

[Eateries List]({{ site.baseurl }}/boise-eateries/) &middot; **Where Should We Eat?** &middot; [Happy Hour Guide]({{ site.baseurl }}/downtown-happy-hour/)

Can't decide? Neither can we, most nights. Hit the button and let it pick from our full list of [Boise-area favorites]({{ site.baseurl }}/boise-eateries/) — if you don't like the answer, tell it "nah" and try again. If it points you downtown, check the [happy hour guide]({{ site.baseurl }}/downtown-happy-hour/) before you go.

<div class="picker">
  <div class="card empty" id="card">
    <div class="name" id="cardName">Ready when you are</div>
  </div>
  <div class="actions">
    <button id="pickBtn" type="button">Pick for me</button>
    <button id="againBtn" type="button" class="secondary" style="display:none;">Nah, hit me again</button>
  </div>
  <p class="count" id="count"></p>
</div>

<div class="history" id="historyWrap" style="display:none;">
  <div class="history-label">Also considered tonight</div>
  <ul id="historyList"></ul>
</div>

<style>
  .picker { margin-top: 24px; }
  .card {
    border: 1px solid #ddd;
    border-radius: 6px;
    background: #f7f7f7;
    padding: 40px 32px;
    text-align: center;
    min-height: 148px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 6px;
  }
  .card.empty { color: #777; font-size: 15px; }
  .card .category {
    font-size: 12px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: #777;
  }
  .card .name {
    font-size: 30px;
    font-weight: 700;
    color: #333;
    transition: opacity 0.15s ease;
  }
  .card .name.rolling { opacity: 0.35; }
  .actions {
    display: flex;
    gap: 12px;
    margin-top: 20px;
    justify-content: center;
    flex-wrap: wrap;
  }
  .picker button {
    font-size: 15px;
    font-weight: 600;
    padding: 11px 20px;
    border-radius: 5px;
    border: 1px solid #333;
    background: #333;
    color: #fff;
    cursor: pointer;
  }
  .picker button:hover { opacity: 0.85; }
  .picker button.secondary {
    background: #fff;
    color: #333;
    border: 1px solid #ddd;
  }
  .picker button.secondary:hover { border-color: #777; opacity: 1; }
  .count {
    margin-top: 20px;
    font-size: 13px;
    color: #777;
    text-align: center;
  }
  .history {
    margin-top: 32px;
    padding-top: 16px;
    border-top: 1px solid #ddd;
  }
  .history-label {
    font-size: 12px;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: #777;
    margin-bottom: 8px;
  }
  .history ul { list-style: none; margin: 0; padding: 0; font-size: 14px; color: #777; }
  .history li { padding: 3px 0; }
</style>

<script>
(function () {
  var PLACES = [{"name": "10 Barrel", "category": "Breweries & Taprooms"}, {"name": "Acero", "category": "Italian"}, {"name": "Albertsons Market Street", "category": "Food Halls & Truck Parks"}, {"name": "Bar Gernika", "category": "European (Basque, German, Spanish)"}, {"name": "Barbarian Brewing", "category": "Breweries & Taprooms"}, {"name": "Bardenay", "category": "Bars & Pubs"}, {"name": "Big Jud's", "category": "Burgers, Drive-Ins & Fast Food"}, {"name": "Biscuit & Hogs", "category": "American, Comfort & Brunch"}, {"name": "Bittercreek Alehouse", "category": "Breweries & Taprooms"}, {"name": "Black Bear Diner", "category": "American, Comfort & Brunch"}, {"name": "Black Moon", "category": "Pizza"}, {"name": "Blaze Pizza", "category": "Pizza"}, {"name": "Boise Fry Company", "category": "Burgers, Drive-Ins & Fast Food"}, {"name": "Bombay Grill", "category": "Indian"}, {"name": "Broad Street Kitchen", "category": "Breweries & Taprooms"}, {"name": "Broken Yolk", "category": "American, Comfort & Brunch"}, {"name": "Burger and Brew", "category": "Burgers, Drive-Ins & Fast Food"}, {"name": "Cafe Ole", "category": "Mexican & Latin American"}, {"name": "Cafe Zupa's", "category": "Sandwiches, Bagels, Bakeries & Sweets"}, {"name": "Chandlers", "category": "Steak & Seafood"}, {"name": "Clairvoyant Brewing", "category": "Breweries & Taprooms"}, {"name": "Cloud 9 Brewery", "category": "Breweries & Taprooms"}, {"name": "Coa de Jima", "category": "Mexican & Latin American"}, {"name": "Cobby's Sandwich Shop", "category": "Sandwiches, Bagels, Bakeries & Sweets"}, {"name": "Corona Village", "category": "Mexican & Latin American"}, {"name": "Crave Kitchen & Bar", "category": "American, Comfort & Brunch"}, {"name": "Double Tap Pub", "category": "Bars & Pubs"}, {"name": "Eight Thirty Common", "category": "American, Comfort & Brunch"}, {"name": "Epi's", "category": "European (Basque, German, Spanish)"}, {"name": "Flying Pie", "category": "Pizza"}, {"name": "Fork", "category": "American, Comfort & Brunch"}, {"name": "Fresh Off The Hook", "category": "Steak & Seafood"}, {"name": "Fujiyama", "category": "Japanese, Sushi & Asian Fusion"}, {"name": "Gil's K-9", "category": "Bars & Pubs"}, {"name": "Ginza Sushi", "category": "Japanese, Sushi & Asian Fusion"}, {"name": "Good Times Bagels", "category": "Sandwiches, Bagels, Bakeries & Sweets"}, {"name": "Goodwood", "category": "BBQ"}, {"name": "Goody's Soda Fountain", "category": "Sandwiches, Bagels, Bakeries & Sweets"}, {"name": "Gramercy Park Pub", "category": "Bars & Pubs"}, {"name": "Grand China Buffet", "category": "Chinese"}, {"name": "Grant's Neighborhood Grill", "category": "American, Comfort & Brunch"}, {"name": "Green Acres Food Truck Park", "category": "Food Halls & Truck Parks"}, {"name": "Grimaldi's", "category": "Pizza"}, {"name": "Gyro Shack", "category": "Mediterranean & Middle Eastern"}, {"name": "Happy Teriyaki", "category": "Japanese, Sushi & Asian Fusion"}, {"name": "Hemlock", "category": "Steak & Seafood"}, {"name": "Holy Cow", "category": "American, Comfort & Brunch"}, {"name": "Hops & Bottles", "category": "Breweries & Taprooms"}, {"name": "Island Sushi", "category": "Japanese, Sushi & Asian Fusion"}, {"name": "Izumi Steakhouse", "category": "Japanese, Sushi & Asian Fusion"}, {"name": "Kahootz", "category": "Bars & Pubs"}, {"name": "Kona Grill", "category": "Hawaiian & Tiki"}, {"name": "Kyoto Palace", "category": "Japanese, Sushi & Asian Fusion"}, {"name": "La Cabinita", "category": "Mexican & Latin American"}, {"name": "Land Ocean", "category": "Steak & Seafood"}, {"name": "Le Peep", "category": "American, Comfort & Brunch"}, {"name": "Little Pearl Oyster Bar", "category": "Steak & Seafood"}, {"name": "Lost Grove Brewing", "category": "Breweries & Taprooms"}, {"name": "Maddie's Wine and Whiskey", "category": "European (Basque, German, Spanish)"}, {"name": "Mai Tai", "category": "Hawaiian & Tiki"}, {"name": "Main Street Burger", "category": "Burgers, Drive-Ins & Fast Food"}, {"name": "Mazzah Mediterranean Grill", "category": "Mediterranean & Middle Eastern"}, {"name": "Mo Betta's", "category": "Hawaiian & Tiki"}, {"name": "MOD Pizza", "category": "Pizza"}, {"name": "Moe Joe's Breakfast Eatery", "category": "American, Comfort & Brunch"}, {"name": "Mongolian BBQ", "category": "Vietnamese, Korean & Mongolian"}, {"name": "Nanzaya", "category": "Japanese, Sushi & Asian Fusion"}, {"name": "Old Chicago", "category": "Pizza"}, {"name": "Owyhee Tavern", "category": "Bars & Pubs"}, {"name": "Percy", "category": "American, Comfort & Brunch"}, {"name": "Pho House", "category": "Vietnamese, Korean & Mongolian"}, {"name": "Pho Nouveau", "category": "Vietnamese, Korean & Mongolian"}, {"name": "Pie Hole", "category": "Pizza"}, {"name": "Pita Pit", "category": "Mediterranean & Middle Eastern"}, {"name": "RAM Brewing", "category": "Breweries & Taprooms"}, {"name": "Red Fort", "category": "Indian"}, {"name": "Red Pavilion", "category": "Chinese"}, {"name": "Reel Foods Fish Market", "category": "Steak & Seafood"}, {"name": "Rotary Sushi", "category": "Japanese, Sushi & Asian Fusion"}, {"name": "Rudy's", "category": "American, Comfort & Brunch"}, {"name": "Sakana", "category": "Japanese, Sushi & Asian Fusion"}, {"name": "Schnitzelgarten", "category": "European (Basque, German, Spanish)"}, {"name": "Seoul Street Cafe", "category": "Vietnamese, Korean & Mongolian"}, {"name": "Sidequest", "category": "Italian"}, {"name": "Smashburger", "category": "Burgers, Drive-Ins & Fast Food"}, {"name": "Smoky Mountain Pizzeria Grill", "category": "Pizza"}, {"name": "Sockeye Brewing", "category": "Breweries & Taprooms"}, {"name": "Stardust Restaurant & Lounge", "category": "American, Comfort & Brunch"}, {"name": "Taj Mahal", "category": "Indian"}, {"name": "Taphouse Pub & Eatery", "category": "Bars & Pubs"}, {"name": "Tarbush Cafe", "category": "Mediterranean & Middle Eastern"}, {"name": "Texas Roadhouse", "category": "Steak & Seafood"}, {"name": "The Basque Center", "category": "European (Basque, German, Spanish)"}, {"name": "The Boise Post", "category": "American, Comfort & Brunch"}, {"name": "The Brickyard", "category": "American, Comfort & Brunch"}, {"name": "The Funky Taco", "category": "Mexican & Latin American"}, {"name": "The Habit", "category": "Burgers, Drive-Ins & Fast Food"}, {"name": "The James Kitchen & Bar", "category": "American, Comfort & Brunch"}, {"name": "The Reef", "category": "Hawaiian & Tiki"}, {"name": "The Warehouse", "category": "Food Halls & Truck Parks"}, {"name": "The Wylder", "category": "Pizza"}, {"name": "Tin Roof Tacos", "category": "Mexican & Latin American"}, {"name": "Tony's Pizzeria Teatro", "category": "Pizza"}, {"name": "Toro's Tacos", "category": "Mexican & Latin American"}, {"name": "Trillium", "category": "American, Comfort & Brunch"}, {"name": "Tupelo Honey", "category": "American, Comfort & Brunch"}, {"name": "UMAI", "category": "Japanese, Sushi & Asian Fusion"}, {"name": "Umami Sushi Burrito", "category": "Japanese, Sushi & Asian Fusion"}, {"name": "Umi Shabu Shabu", "category": "Japanese, Sushi & Asian Fusion"}, {"name": "Voodoo Brewing", "category": "Breweries & Taprooms"}, {"name": "Westside Drive In", "category": "Burgers, Drive-Ins & Fast Food"}, {"name": "Wyld Child", "category": "Bars & Pubs"}, {"name": "Yard House", "category": "American, Comfort & Brunch"}, {"name": "Yen Ching", "category": "Chinese"}, {"name": "Yoi Tomo", "category": "Japanese, Sushi & Asian Fusion"}];

  var card = document.getElementById('card');
  var cardName = document.getElementById('cardName');
  var pickBtn = document.getElementById('pickBtn');
  var againBtn = document.getElementById('againBtn');
  var countEl = document.getElementById('count');
  var historyWrap = document.getElementById('historyWrap');
  var historyList = document.getElementById('historyList');

  var last = null;
  var history = [];
  var categoryEl = null;

  function pick() {
    var choice;
    do {
      choice = PLACES[Math.floor(Math.random() * PLACES.length)];
    } while (PLACES.length > 1 && last && choice.name === last.name);

    cardName.classList.add('rolling');
    setTimeout(function () {
      card.classList.remove('empty');
      if (!categoryEl) {
        categoryEl = document.createElement('div');
        categoryEl.className = 'category';
        card.insertBefore(categoryEl, cardName);
      }
      categoryEl.textContent = choice.category;
      cardName.textContent = choice.name;
      cardName.classList.remove('rolling');
    }, 120);

    if (last) {
      history.unshift(last);
      history = history.slice(0, 5);
    }
    last = choice;

    pickBtn.style.display = 'none';
    againBtn.style.display = 'inline-block';
    countEl.textContent = PLACES.length + ' places on the list';

    if (history.length) {
      historyWrap.style.display = 'block';
      historyList.innerHTML = history.map(function (h) {
        return '<li>' + h.name + ' &mdash; ' + h.category + '</li>';
      }).join('');
    }
  }

  pickBtn.addEventListener('click', pick);
  againBtn.addEventListener('click', pick);
})();
</script>
