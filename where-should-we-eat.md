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

*The lunch/dinner/happy hour tags below are our best-guess categorization, not verified per-restaurant — treat them as a rough filter, not a guarantee.*

<div class="filters">
  <label><input type="checkbox" class="filter-cb" value="lunch"> Lunch</label>
  <label><input type="checkbox" class="filter-cb" value="dinner"> Dinner</label>
  <label><input type="checkbox" class="filter-cb" value="happyHour"> Happy Hour</label>
</div>

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
  .filters {
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
    margin-top: 20px;
    padding: 14px 16px;
    background: #f7f7f7;
    border: 1px solid #ddd;
    border-radius: 6px;
    font-size: 14px;
  }
  .filters label {
    display: flex;
    align-items: center;
    gap: 6px;
    cursor: pointer;
    color: #333;
  }
  .filters input[type="checkbox"] {
    width: 16px;
    height: 16px;
    cursor: pointer;
  }
  .picker { margin-top: 16px; }
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
  .picker button:disabled { opacity: 0.4; cursor: not-allowed; }
  .picker button:hover:not(:disabled) { opacity: 0.85; }
  .picker button.secondary {
    background: #fff;
    color: #333;
    border: 1px solid #ddd;
  }
  .picker button.secondary:hover:not(:disabled) { border-color: #777; opacity: 1; }
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
  var PLACES = [{"name": "10 Barrel", "category": "Breweries & Taprooms", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Acero", "category": "Italian", "lunch": false, "dinner": true, "happyHour": false}, {"name": "Albertsons Market Street", "category": "Food Halls & Truck Parks", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Bar Gernika", "category": "European (Basque, German, Spanish)", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Barbarian Brewing", "category": "Breweries & Taprooms", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Bardenay", "category": "Bars & Pubs", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Big Jud's", "category": "Burgers, Drive-Ins & Fast Food", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Biscuit & Hogs", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Bittercreek Alehouse", "category": "Breweries & Taprooms", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Black Bear Diner", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Black Moon", "category": "Pizza", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Blaze Pizza", "category": "Pizza", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Boise Fry Company", "category": "Burgers, Drive-Ins & Fast Food", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Bombay Grill", "category": "Indian", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Broad Street Kitchen", "category": "Breweries & Taprooms", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Broken Yolk", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Burger and Brew", "category": "Burgers, Drive-Ins & Fast Food", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Cafe Ole", "category": "Mexican & Latin American", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Cafe Zupa's", "category": "Sandwiches, Bagels, Bakeries & Sweets", "lunch": true, "dinner": false, "happyHour": false}, {"name": "Chandlers", "category": "Steak & Seafood", "lunch": false, "dinner": true, "happyHour": false}, {"name": "Clairvoyant Brewing", "category": "Breweries & Taprooms", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Cloud 9 Brewery", "category": "Breweries & Taprooms", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Coa de Jima", "category": "Mexican & Latin American", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Cobby's Sandwich Shop", "category": "Sandwiches, Bagels, Bakeries & Sweets", "lunch": true, "dinner": false, "happyHour": false}, {"name": "Corona Village", "category": "Mexican & Latin American", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Crave Kitchen & Bar", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Das Alpenhaus Delikatessen", "category": "European (Basque, German, Spanish)", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Don & Charly's", "category": "Sandwiches, Bagels, Bakeries & Sweets", "lunch": true, "dinner": false, "happyHour": false}, {"name": "Double Tap Pub", "category": "Bars & Pubs", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Eight Thirty Common", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Epi's", "category": "European (Basque, German, Spanish)", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Flying Pie", "category": "Pizza", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Fork", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Fresh Off The Hook", "category": "Steak & Seafood", "lunch": false, "dinner": true, "happyHour": false}, {"name": "Fujiyama", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Gil's K-9", "category": "Bars & Pubs", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Ginza Sushi", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Good Times Bagels", "category": "Sandwiches, Bagels, Bakeries & Sweets", "lunch": true, "dinner": false, "happyHour": false}, {"name": "Goodwood", "category": "BBQ", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Goody's Soda Fountain", "category": "Sandwiches, Bagels, Bakeries & Sweets", "lunch": true, "dinner": false, "happyHour": false}, {"name": "Gramercy Park Pub", "category": "Bars & Pubs", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Grand China Buffet", "category": "Chinese", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Grant's Neighborhood Grill", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Green Acres Food Truck Park", "category": "Food Halls & Truck Parks", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Grimaldi's", "category": "Pizza", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Gyro Shack", "category": "Mediterranean & Middle Eastern", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Happy Teriyaki", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Hemlock", "category": "Steak & Seafood", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Holy Cow", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Hops & Bottles", "category": "Breweries & Taprooms", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Island Sushi", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Izumi Steakhouse", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Kahootz", "category": "Bars & Pubs", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Kona Grill", "category": "Hawaiian & Tiki", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Kyoto Palace", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}, {"name": "La Cabinita", "category": "Mexican & Latin American", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Land Ocean", "category": "Steak & Seafood", "lunch": false, "dinner": true, "happyHour": false}, {"name": "Le Peep", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Little Pearl Oyster Bar", "category": "Steak & Seafood", "lunch": false, "dinner": true, "happyHour": false}, {"name": "Lost Grove Brewing", "category": "Breweries & Taprooms", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Maddie's Wine and Whiskey", "category": "European (Basque, German, Spanish)", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Mai Tai", "category": "Hawaiian & Tiki", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Main Street Burger", "category": "Burgers, Drive-Ins & Fast Food", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Mazzah Mediterranean Grill", "category": "Mediterranean & Middle Eastern", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Mo Betta's", "category": "Hawaiian & Tiki", "lunch": true, "dinner": true, "happyHour": true}, {"name": "MOD Pizza", "category": "Pizza", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Moe Joe's Breakfast Eatery", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Mongolian BBQ", "category": "Vietnamese, Korean & Mongolian", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Nanzaya", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Old Chicago", "category": "Pizza", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Owyhee Tavern", "category": "Bars & Pubs", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Percy", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Pho House", "category": "Vietnamese, Korean & Mongolian", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Pho Nouveau", "category": "Vietnamese, Korean & Mongolian", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Pie Hole", "category": "Pizza", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Pita Pit", "category": "Mediterranean & Middle Eastern", "lunch": true, "dinner": true, "happyHour": false}, {"name": "RAM Brewing", "category": "Breweries & Taprooms", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Red Fort", "category": "Indian", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Red Pavilion", "category": "Chinese", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Reel Foods Fish Market", "category": "Steak & Seafood", "lunch": false, "dinner": true, "happyHour": false}, {"name": "Rotary Sushi", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Rudy's", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Sakana", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Schnitzelgarten", "category": "European (Basque, German, Spanish)", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Seoul Street Cafe", "category": "Vietnamese, Korean & Mongolian", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Sidequest", "category": "Italian", "lunch": false, "dinner": true, "happyHour": false}, {"name": "Smashburger", "category": "Burgers, Drive-Ins & Fast Food", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Smoky Mountain Pizzeria Grill", "category": "Pizza", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Sockeye Brewing", "category": "Breweries & Taprooms", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Stardust Restaurant & Lounge", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Taj Mahal", "category": "Indian", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Taphouse Pub & Eatery", "category": "Bars & Pubs", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Tarbush Cafe", "category": "Mediterranean & Middle Eastern", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Texas Roadhouse", "category": "Steak & Seafood", "lunch": false, "dinner": true, "happyHour": false}, {"name": "The Basque Center", "category": "European (Basque, German, Spanish)", "lunch": false, "dinner": true, "happyHour": true}, {"name": "The Boise Post", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "The Brickyard", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "The Funky Taco", "category": "Mexican & Latin American", "lunch": true, "dinner": true, "happyHour": true}, {"name": "The Habit", "category": "Burgers, Drive-Ins & Fast Food", "lunch": true, "dinner": true, "happyHour": false}, {"name": "The James Kitchen & Bar", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "The Reef", "category": "Hawaiian & Tiki", "lunch": true, "dinner": true, "happyHour": true}, {"name": "The Warehouse", "category": "Food Halls & Truck Parks", "lunch": true, "dinner": true, "happyHour": true}, {"name": "The Wylder", "category": "Pizza", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Tin Roof Tacos", "category": "Mexican & Latin American", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Tony's Pizzeria Teatro", "category": "Pizza", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Toro's Tacos", "category": "Mexican & Latin American", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Trillium", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Tupelo Honey", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": false}, {"name": "UMAI", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Umami Sushi Burrito", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Umi Shabu Shabu", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Voodoo Brewing", "category": "Breweries & Taprooms", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Westside Drive In", "category": "Burgers, Drive-Ins & Fast Food", "lunch": true, "dinner": true, "happyHour": false}, {"name": "Wyld Child", "category": "Bars & Pubs", "lunch": false, "dinner": true, "happyHour": true}, {"name": "Yard House", "category": "American, Comfort & Brunch", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Yen Ching", "category": "Chinese", "lunch": true, "dinner": true, "happyHour": true}, {"name": "Yoi Tomo", "category": "Japanese, Sushi & Asian Fusion", "lunch": true, "dinner": true, "happyHour": false}];

  var card = document.getElementById('card');
  var cardName = document.getElementById('cardName');
  var pickBtn = document.getElementById('pickBtn');
  var againBtn = document.getElementById('againBtn');
  var countEl = document.getElementById('count');
  var historyWrap = document.getElementById('historyWrap');
  var historyList = document.getElementById('historyList');
  var filterBoxes = Array.prototype.slice.call(document.querySelectorAll('.filter-cb'));

  var last = null;
  var history = [];
  var categoryEl = null;

  function getFiltered() {
    var active = filterBoxes.filter(function (cb) { return cb.checked; }).map(function (cb) { return cb.value; });
    if (!active.length) return PLACES;
    return PLACES.filter(function (p) {
      return active.some(function (key) { return p[key]; });
    });
  }

  function updateCount() {
    var pool = getFiltered();
    if (pool.length) {
      countEl.textContent = pool.length + ' place' + (pool.length === 1 ? '' : 's') + ' match' + (pool.length === 1 ? 'es' : '') + ' your filters';
      pickBtn.disabled = false;
    } else {
      countEl.textContent = 'No places match those filters — try unchecking one';
      pickBtn.disabled = true;
      againBtn.disabled = true;
    }
  }

  function pick() {
    var pool = getFiltered();
    if (!pool.length) return;
    var choice;
    do {
      choice = pool[Math.floor(Math.random() * pool.length)];
    } while (pool.length > 1 && last && choice.name === last.name);

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
    againBtn.disabled = false;
    updateCount();

    if (history.length) {
      historyWrap.style.display = 'block';
      historyList.innerHTML = history.map(function (h) {
        return '<li>' + h.name + ' &mdash; ' + h.category + '</li>';
      }).join('');
    }
  }

  filterBoxes.forEach(function (cb) {
    cb.addEventListener('change', function () {
      last = null;
      history = [];
      historyWrap.style.display = 'none';
      card.classList.add('empty');
      if (categoryEl) { categoryEl.remove(); categoryEl = null; }
      cardName.textContent = 'Ready when you are';
      pickBtn.style.display = 'inline-block';
      againBtn.style.display = 'none';
      updateCount();
    });
  });

  pickBtn.addEventListener('click', pick);
  againBtn.addEventListener('click', pick);
  updateCount();
})();
</script>
