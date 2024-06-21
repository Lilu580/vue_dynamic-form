Dynamic Form with Vue 3 and Tailwind CSS
This project is a dynamic form built with Vue 3, Vite, and Tailwind CSS. The form allows users to add and remove input fields dynamically, count vowels in each field, and highlight fields based on a search query.

Features
Dynamic Fields: Add up to 10 input fields. Each field has a button to remove it if there are more than one field.
Vowel Count: Displays the count of vowels (a, e, i, o, u) in each input field.
Search Functionality: A search field at the top highlights any input field that contains the entered text. If the search text matches any text in the input fields, the search field itself is highlighted.
Installation
Clone the repository:

git clone https://github.com/Lilu580/vue_dynamic-form.git
cd dynamic-form

Install dependencies:

npm install

Run the development server:

npm run dev
Usage
Adding Fields:

Click the "Add Field" button to add a new input field.
You can add up to a maximum of 10 fields.
Removing Fields:

Click the "Remove" button next to an input field to remove it.
At least one field must remain.
Counting Vowels:

Each input field displays the count of vowels in real-time as you type.
Search Functionality:

Enter text in the search field at the top.
Fields containing the search text are highlighted with a green background.
If the search text matches any field, the search field is highlighted green. If no match is found, the search field is highlighted green.

Technologies Used
Vue 3: Frontend framework used to build the dynamic form.
Vite: Build tool that provides fast setup and development.
Tailwind CSS: Utility-first CSS framework used for styling.
TypeScript: For type checking and better developer experience.
Contributing
Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.

License
This project is licensed under the MIT License. See the LICENSE file for details.

Contact
For any questions or inquiries, please contact [bogdanmaliutawork@gmail.com].