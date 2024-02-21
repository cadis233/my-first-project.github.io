<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Login</title>
  <style>
    .hidden {
      display: none;
    }
  </style>
</head>
<body>
  <h1>Аутентификация</h1>

  <div id="loginForm">
    <input type="text" id="username" placeholder="Логин">
    <input type="password" id="password" placeholder="Пароль">
    <button onclick="login()">Войти</button>
  </div>

  <div id="adminFunctionality" class="hidden">
        <button onclick="logoutAdmin()">Выйти из учетной записи</button>
    </body>

    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <link rel="stylesheet" href="styles.css">
      <title>Список элементов</title>
    </head>

    <body>
      <h1>Список элементов</h1>
      <input type="text" id="inputField" pattern="[A-Za-zА-Яа-я0-9]{1,4}" title="Можно вводить только русские и латинские строчные буквы, числа от 0 до 9999" placeholder="Введите элемент">
      <button onclick="addItem()">Добавить</button>
      <div id="itemList"></div>
      <p id="itemCount">Количество элементов: 0</p>
      <button onclick="clearList()">Удалить список</button>
    <button onclick="filterAll()">Все элементы</button>
    <button onclick="filter0to100()">0-100</button>
    <button onclick="filter101to200()">101-200</button>
    <button onclick="filter201to300()">201-300</button>
    <button onclick="filter300to9999()">300-9 999</button>
    <button onclick="filterAToM()">A-M</button>
    <button onclick="filterNToZ()">N-Z</button>
    <button onclick="filterRussianAToN()">А-Н</button>
    <button onclick="filterRussianOToYa()">О-Я</button>
    <button onclick="filterOnlyLetters()">Только буквы</button>
    <button onclick="filterOnlyNumbers()">Только числа</button>

    <button onclick="sortAscending()">По возрастанию</button>
    <button onclick="sortDescending()">По убыванию</button>

      <button onclick="saveToFile()">Сохранить в файл</button>
      <input type="file" onchange="openFromFile(this)" />
      <button onclick="closeApp()">Закрыть программу</button>
      <script src="script.js"></script>
      <style>
        body {
          font-family: Arial, sans-serif;
          text-align: center;
          background-color: #f7f7f7;
        }

        input, button {
          margin: 5px;
        }

        button {
          padding: 10px 20px;
          border: none;
          background-color: #d9534f;
          color: white;
          cursor: pointer;
          transition: background-color 0.3s ease;
        }

        button:hover {
          background-color: #c9302c;
        }

        #itemList {
          margin-top: 20px;
          text-align: left;
        }

        .item {
          padding: 10px;
          margin: 5px;
          background-color: #f2dede;
          border: 1px solid #ebccd1;
          color: #a94442;
          display: flex;
          justify-content: space-between;
          align-items: center;
        }

        .item button {
          background-color: #d9534f;
          color: white;
          border: none;
          padding: 5px 10px;
          cursor: pointer;
          transition: background-color 0.3s ease;
        }

        .item button:hover {
          background-color: #c9302c;
        }

        #itemCount {
          margin-top: 20px;
          font-weight: bold;
          color: #d9534f;
        }

      </style>
  <script>
    let items = [];
    
    function addItem() {
      let input = document.getElementById('inputField').value;
      if (/[^A-Za-zА-Яа-я0-9]/.test(input) || parseInt(input) < 0 || parseInt(input) > 9999) {
        alert("Ошибка! Можно вводить только русские и латинские строчные буквы, числа от 0 до 9999");
      } else if (input !== '') {
        items.push(input);
        displayItems();
        updateItemCount();
      }
    }

    function displayItems() {
      let itemList = document.getElementById('itemList');
      itemList.innerHTML = '';
      items.forEach(item => {
        let element = document.createElement('div');
        element.textContent = item;
        let deleteButton = document.createElement('button');
        deleteButton.textContent = 'Удалить';
        deleteButton.onclick = function() {
          deleteItem(item);
        };
        element.appendChild(deleteButton);
        itemList.appendChild(element);
      });
    }

    function deleteItem(item) {
      let index = items.indexOf(item);
      if (index > -1) {
        items.splice(index, 1);
        displayItems();
        updateItemCount();
      }
    }

    function clearList() {
      items = [];
      displayItems();
      updateItemCount();
    }

    function updateItemCount() {
      let count = items.length;
      document.getElementById('itemCount').textContent = `Количество элементов: ${count}`;
    }
    function filterAll() {
      displayItems();
    }
    function displayFilteredItems(filteredItems) {
      let itemList = document.getElementById('itemList');
      itemList.innerHTML = '';
      filteredItems.forEach(item => {
        let element = document.createElement('div');
        element.textContent = item;
        let deleteButton = document.createElement('button');
        deleteButton.textContent = 'Удалить';
        deleteButton.onclick = function() {
          deleteItem(item);
        };
        element.appendChild(deleteButton);
        itemList.appendChild(element);
      });
    }
function filter0to100() {
  let filteredItems = items.filter(item => !isNaN(item) && parseInt(item) >= 0 && parseInt(item) <= 100);
  displayFilteredItems(filteredItems);
}

function filter101to200() {
  let filteredItems = items.filter(item => !isNaN(item) && parseInt(item) >= 101 && parseInt(item) <= 200);
  displayFilteredItems(filteredItems);
}

function filter201to300() {
  let filteredItems = items.filter(item => !isNaN(item) && parseInt(item) >= 201 && parseInt(item) <= 300);
  displayFilteredItems(filteredItems);
}

function filter300to9999() {
  let filteredItems = items.filter(item => !isNaN(item) && parseInt(item) >= 300 && parseInt(item) <= 9999);
  displayFilteredItems(filteredItems);
}

function filterAToM() {
  let filteredItems = items.filter(item => /[a-m]/i.test(item));
  displayFilteredItems(filteredItems);
}

function filterNToZ() {
  let filteredItems = items.filter(item => /[n-z]/i.test(item));
  displayFilteredItems(filteredItems);
}

function filterRussianAToN() {
  let filteredItems = items.filter(item => /[а-н]/i.test(item));
  displayFilteredItems(filteredItems);
}

function filterRussianOToYa() {
  let filteredItems = items.filter(item => /[о-я]/i.test(item));
  displayFilteredItems(filteredItems);
}

function filterOnlyLetters() {
  let filteredItems = items.filter(item => /^[a-zA-Zа-яА-Я]+$/.test(item));
  displayFilteredItems(filteredItems);
}

function filterOnlyNumbers() {
  let filteredItems = items.filter(item => /^\d+$/.test(item));
  displayFilteredItems(filteredItems);
}

function sortAscending() {
  items.sort((a, b) => a.localeCompare(b, 'ru', { numeric: true }));
  displayItems();
}

function sortDescending() {
  items.sort((a, b) => b.localeCompare(a, 'ru', { numeric: true }));
  displayItems();
}

function saveToFile() {
  let itemsToSave = items.join('\n');
  let blob = new Blob([itemsToSave], { type: "text/plain;charset=utf-8" });

  // Создаем ссылку на объект Blob
  let link = document.createElement("a");
  link.href = URL.createObjectURL(blob);

  // Устанавливаем атрибут загрузки и имя файла
  link.download = "itemList.txt";

  // Добавляем ссылку в DOM и эмулируем клик по ней
  document.body.appendChild(link);
  link.click();

  // Чистим ссылку из DOM
  document.body.removeChild(link);
}

function openFromFile(input) {
  const file = input.files[0];
  const reader = new FileReader();
  reader.onload = function(e) {
    const contents = e.target.result;
    items = contents.split('\n').map(item => item.trim());
    displayItems();
  };
  reader.readAsText(file);
}

function closeApp() {
  window.close();
}

  </script>
  </div>
      <div id="userFunctionality" class="hidden">

      <!DOCTYPE html>
      <html lang="ru">
      <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <link rel="stylesheet" href="styles.css">
        <title>Список элементов</title>
        <style>
          <style>
            body {
              font-family: Arial, sans-serif;
              text-align: center;
              background-color: #f7f7f7;
            }

            input, button {
              margin: 5px;
            }

            button {
              padding: 10px 20px;
              border: none;
              background-color: #d9534f;
              color: white;
              cursor: pointer;
              transition: background-color 0.3s ease;
            }

            button:hover {
              background-color: #c9302c;
            }

            #itemList {
              margin-top: 20px;
              text-align: left;
            }

            .item {
              padding: 10px;
              margin: 5px;
              background-color: #f2dede;
              border: 1px solid #ebccd1;
              color: #9b2d30;
              display: flex;
              justify-content: space-between;
              align-items: center;
            }

            .item button {
              background-color: #d9534f;
              color: white;
              border: none;
              padding: 5px 10px;
              cursor: pointer;
              transition: background-color 0.3s ease;
            }

            .item button:hover {
              background-color: #c9302c;
            }

            #itemCount {
              margin-top: 20px;
              font-weight: bold;
              color: #d9534f;
            }

          </style>
        </style>
      </head>

        <head>
    <body>
      <button onclick="logoutUser()">Выйти из учетной записи</button>

      <h1>Список элементов</h1>

      <input type="text" id="inputField" pattern="[A-Za-zА-Яа-я0-9]{1,4}" title="Можно вводить только русские и латинские строчные буквы, числа от 0 до 9999" placeholder="Введите элемент">
      <button onclick="addItem()">Добавить</button>
      <div id="itemList"></div>
      <p id="itemCount">Количество элементов: 0</p>
      <button onclick="clearList()">Удалить список</button>
    <button onclick="filterAll()">Все элементы</button>
    <button onclick="filter0to100()">0-100</button>
    <button onclick="filter101to200()">101-200</button>
    <button onclick="filter201to300()">201-300</button>
    <button onclick="filter300to9999()">300-9 999</button>
    <button onclick="filterAToM()">A-M</button>
    <button onclick="filterNToZ()">N-Z</button>
    <button onclick="filterRussianAToN()">А-Н</button>
    <button onclick="filterRussianOToYa()">О-Я</button>
    <button onclick="filterOnlyLetters()">Только буквы</button>
    <button onclick="filterOnlyNumbers()">Только числа</button>

    <button onclick="sortAscending()">По возрастанию</button>
    <button onclick="sortDescending()">По убыванию</button>


      <button onclick="closeApp()">Закрыть программу</button>
      <script src="script.js"></script>
     
  <script>


    function addItem() {
      let input = document.getElementById('inputField').value;
      if (/[^A-Za-zА-Яа-я0-9]/.test(input) || parseInt(input) < 0 || parseInt(input) > 9999) {
        alert("Ошибка! Можно вводить только русские и латинские строчные буквы, числа от 0 до 9999");
      } else if (input !== '') {
        items.push(input);
        displayItems();
        updateItemCount();
      }
    }

    function displayItems() {
      let itemList = document.getElementById('itemList');
      itemList.innerHTML = '';
      items.forEach(item => {
        let element = document.createElement('div');
        element.textContent = item;
        let deleteButton = document.createElement('button');
        deleteButton.textContent = 'Удалить';
        deleteButton.onclick = function() {
          deleteItem(item);
        };
        element.appendChild(deleteButton);
        itemList.appendChild(element);
      });
    }

    function deleteItem(item) {
      let index = items.indexOf(item);
      if (index > -1) {
        items.splice(index, 1);
        displayItems();
        updateItemCount();
      }
    }

    function clearList() {
      items = [];
      displayItems();
      updateItemCount();
    }

    function updateItemCount() {
      let count = items.length;
      document.getElementById('itemCount').textContent = `Количество элементов: ${count}`;
    }

    function filterAll() {
      displayItems();
    }
    function displayFilteredItems(filteredItems) {
      let itemList = document.getElementById('itemList');
      itemList.innerHTML = '';
      filteredItems.forEach(item => {
        let element = document.createElement('div');
        element.textContent = item;
        let deleteButton = document.createElement('button');
        deleteButton.textContent = 'Удалить';
        deleteButton.onclick = function() {
          deleteItem(item);
        };
        element.appendChild(deleteButton);
        itemList.appendChild(element);
      });
    }
function filter0to100() {
  let filteredItems = items.filter(item => !isNaN(item) && parseInt(item) >= 0 && parseInt(item) <= 100);
  displayFilteredItems(filteredItems);
}

function filter101to200() {
  let filteredItems = items.filter(item => !isNaN(item) && parseInt(item) >= 101 && parseInt(item) <= 200);
  displayFilteredItems(filteredItems);
}

function filter201to300() {
  let filteredItems = items.filter(item => !isNaN(item) && parseInt(item) >= 201 && parseInt(item) <= 300);
  displayFilteredItems(filteredItems);
}

function filter300to9999() {
  let filteredItems = items.filter(item => !isNaN(item) && parseInt(item) >= 300 && parseInt(item) <= 9999);
  displayFilteredItems(filteredItems);
}

function filterAToM() {
  let filteredItems = items.filter(item => /[a-m]/i.test(item));
  displayFilteredItems(filteredItems);
}

function filterNToZ() {
  let filteredItems = items.filter(item => /[n-z]/i.test(item));
  displayFilteredItems(filteredItems);
}

function filterRussianAToN() {
  let filteredItems = items.filter(item => /[а-н]/i.test(item));
  displayFilteredItems(filteredItems);
}

function filterRussianOToYa() {
  let filteredItems = items.filter(item => /[о-я]/i.test(item));
  displayFilteredItems(filteredItems);
}

function filterOnlyLetters() {
  let filteredItems = items.filter(item => /^[a-zA-Zа-яА-Я]+$/.test(item));
  displayFilteredItems(filteredItems);
}

function filterOnlyNumbers() {
  let filteredItems = items.filter(item => /^\d+$/.test(item));
  displayFilteredItems(filteredItems);
}

function sortAscending() {
  items.sort((a, b) => a.localeCompare(b, 'ru', { numeric: true }));
  displayItems();
}

function sortDescending() {
  items.sort((a, b) => b.localeCompare(a, 'ru', { numeric: true }));
  displayItems();
}

function closeApp() {
  window.close();
}

  </script>
        </body>

       </head>
      <script src="script.js"></script>
 
    </html>
        </div>


  <div id="guestFunctionality" class="hidden">
    <!-- Функциональность для гостя -->


    <button onclick="logoutGuest()">Выйти из учетной записи</button>

  <body>
    <h1>Список элементов</h1>
    <p id="itemCount">Количество элементов: 0</p>

  <button onclick="filterAll()">Все элементы</button>
  <button onclick="filter0to100()">0-100</button>
  <button onclick="filter101to200()">101-200</button>
  <button onclick="filter201to300()">201-300</button>
  <button onclick="filter300to9999()">300-9 999</button>
  <button onclick="filterAToM()">A-M</button>
  <button onclick="filterNToZ()">N-Z</button>
  <button onclick="filterRussianAToN()">А-Н</button>
  <button onclick="filterRussianOToYa()">О-Я</button>
  <button onclick="filterOnlyLetters()">Только буквы</button>
  <button onclick="filterOnlyNumbers()">Только числа</button>

  <button onclick="sortAscending()">По возрастанию</button>
  <button onclick="sortDescending()">По убыванию</button>
  <input type="file" onchange="openFromFile(this)" />

    <style>
      body {
        font-family: Arial, sans-serif;
        text-align: center;
        background-color: #f7f7f7;
      }

      input, button {
        margin: 5px;
      }

      button {
        padding: 10px 20px;
        border: none;
        background-color: #d9534f;
        color: white;
        cursor: pointer;
        transition: background-color 0.3s ease;
      }

      button:hover {
        background-color: #c9302c;
      }

      #itemList {
        margin-top: 20px;
        text-align: left;
      }

      .item {
        padding: 10px;
        margin: 5px;
        background-color: #f2dede;
        border: 1px solid #ebccd1;
        color: #a94442;
        display: flex;
        justify-content: space-between;
        align-items: center;
      }

      .item button {
        background-color: #d9534f;
        color: white;
        border: none;
        padding: 5px 10px;
        cursor: pointer;
        transition: background-color 0.3s ease;
      }

      .item button:hover {
        background-color: #c9302c;
      }

      #itemCount {
        margin-top: 20px;
        font-weight: bold;
        color: #d9534f;
      }

    </style>


<script>


    function updateItemCount() {
      let count = items.length;
      document.getElementById('itemCount').textContent = `Количество элементов: ${count}`;
    }

    function filterAll() {
      displayItems();
    }
  
  function displayFilteredItems(filteredItems) {
    let itemList = document.getElementById('itemList');
    itemList.innerHTML = '';
    filteredItems.forEach(item => {
      let element = document.createElement('div');
      element.textContent = item;
      let deleteButton = document.createElement('button');
      deleteButton.textContent = 'Удалить';
      deleteButton.onclick = function() {
        deleteItem(item);
      };
      element.appendChild(deleteButton);
      itemList.appendChild(element);
    });
  }
function filter0to100() {
  let filteredItems = items.filter(item => !isNaN(item) && parseInt(item) >= 0 && parseInt(item) <= 100);
  displayFilteredItems(filteredItems);
}

function filter101to200() {
  let filteredItems = items.filter(item => !isNaN(item) && parseInt(item) >= 101 && parseInt(item) <= 200);
  displayFilteredItems(filteredItems);
}

function filter201to300() {
  let filteredItems = items.filter(item => !isNaN(item) && parseInt(item) >= 201 && parseInt(item) <= 300);
  displayFilteredItems(filteredItems);
}

function filter300to9999() {
  let filteredItems = items.filter(item => !isNaN(item) && parseInt(item) >= 300 && parseInt(item) <= 9999);
  displayFilteredItems(filteredItems);
}

function filterAToM() {
  let filteredItems = items.filter(item => /[a-m]/i.test(item));
  displayFilteredItems(filteredItems);
}

function filterNToZ() {
  let filteredItems = items.filter(item => /[n-z]/i.test(item));
  displayFilteredItems(filteredItems);
}

function filterRussianAToN() {
  let filteredItems = items.filter(item => /[а-н]/i.test(item));
  displayFilteredItems(filteredItems);
}

function filterRussianOToYa() {
  let filteredItems = items.filter(item => /[о-я]/i.test(item));
  displayFilteredItems(filteredItems);
}

function filterOnlyLetters() {
  let filteredItems = items.filter(item => /^[a-zA-Zа-яА-Я]+$/.test(item));
  displayFilteredItems(filteredItems);
}

function filterOnlyNumbers() {
  let filteredItems = items.filter(item => /^\d+$/.test(item));
  displayFilteredItems(filteredItems);
}

function sortAscending() {
  items.sort((a, b) => a.localeCompare(b, 'ru', { numeric: true }));
  displayItems();
}

function sortDescending() {
  items.sort((a, b) => b.localeCompare(a, 'ru', { numeric: true }));
  displayItems();
}
  function openFromFile(input) {
    const file = input.files[0];
    const reader = new FileReader();
    reader.onload = function(e) {
      const contents = e.target.result;
      items = contents.split('\n').map(item => item.trim());
      displayItems();
    };
    reader.readAsText(file);
  }

  </script>
</body>

  </div>

  <script>
    function login() {
      var username = document.getElementById('username').value;
      var password = document.getElementById('password').value;
      
      if (username === 'admin' && password === 'pass1') {
        // Аутентификация администратора
        document.getElementById('loginForm').classList.add('hidden');
        document.getElementById('adminFunctionality').classList.remove('hidden');
      } else if (username === 'user' && password === 'pass2') {
        // Аутентификация обычного пользователя
        document.getElementById('loginForm').classList.add('hidden');
        document.getElementById('userFunctionality').classList.remove('hidden');
      } else if (username === 'guest' && password === 'pass3') {
        // Аутентификация гостя
        document.getElementById('loginForm').classList.add('hidden');
        document.getElementById('guestFunctionality').classList.remove('hidden');
      } else {
        alert('Неверный логин или пароль');
      }
    }
        function logoutAdmin() {
      // Логика выхода для администратора
      alert('ВЫ УБЕРЕНЫ, admin????');
      window.location.reload();
    }

    function logoutUser() {
      // Логика выхода для обычного пользователя
      alert('ВЫ УБЕРЕНЫ, user????');
      window.location.reload();
    }

    function logoutGuest() {
      // Логика выхода для гостя
      alert('ВЫ УБЕРЕНЫ, guest????');
      window.location.reload();
    }
  </script>
</body>
</html>
