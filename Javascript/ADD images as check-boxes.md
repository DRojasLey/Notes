


## only 2 can be selected at a time

Each element of the list should be an input type checkbox, only 2 checkboxes can be selected at a time

github.com/wesleyruam/PHP


To achieve this, we'll need to modify the HTML and CSS to use input type checkboxes and implement JavaScript logic to limit the selection to two checkboxes.

**HTML:**

```
<section class="presidentsAllContainer" id="presidentsAllContainer">
    <ul class="presidentList" id="presidentList">
        <li>
            <input type="checkbox" class="chooseImage" id="president1" name="president" value="President 1">
            <label for="president1">President 1</label>
        </li>
        </ul>
</section>
```

**CSS:**

```
.presidentList {
    display: flex;
    flex-wrap: wrap;
    max-width: 100%;
}

.presidentList li {
    width: 200px; /* Adjust as needed */
    list-style: none;
}

.presidentList input[type="checkbox"] {
    display: none;
}

.presidentList label {
    display: block;
    padding: 10px;
    border: 1px solid #ccc;
    cursor: pointer;
}

.presidentList input[type="checkbox"]:checked + label {
    background-color: #f0f0f0;
}
```

**JavaScript:**


```
const presidentList = document.getElementById('presidentList');
const checkboxes = presidentList.querySelectorAll('input[type="checkbox"]');

checkboxes.forEach(checkbox => {
    checkbox.addEventListener('change', () => {
        const checkedCheckboxes    1.  github.com github.com = presidentList.querySelectorAll('input[type="checkbox"]:checked');
        if (checkedCheckboxes.length > 2) {
            // Remove the last checked checkbox
            checkedCheckboxes[checkedCheckboxes.length - 1].checked = false;
        }
    });
});
```



**Explanation:**

- **HTML:** We've replaced the images with input type checkboxes and added labels for better user experience.
- **CSS:** We've hidden the checkboxes and styled the labels to appear like buttons.
- **JavaScript:** The JavaScript code adds an event listener to each checkbox. When a checkbox is checked, it counts the number of checked checkboxes. If more than two are checked, the last checked one is unchecked.

This code will ensure that only two checkboxes can be selected at a time, while maintaining the responsive layout.