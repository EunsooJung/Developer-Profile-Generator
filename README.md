# Developer-Profile-Generator

Created a command-line application that dynamically generates a PDF profile from a GitHub username.

- Built a Developer Profile Generator using the GitHub API
- [Applied to My Reponsive Portfolio](https://eunsoojung.github.io/Unit-02-Responsive-Portfolio/portfolio.html)

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

```bash
# Install puppeteer
npm i puppeteer

# Run
node index.js
```

## Preview

[![Developer Profile Generator](https://github.com/EunsooJung/Developer-Profile-Generator/blob/master/assets/09-Dev-Profile-Gen.png)](https://github.com/EunsooJung/Developer-Profile-Generator/blob/master/assets/09-Dev-Profile-Gen.png)

## Usage

### Basic Usage

After downloading, simply edit the HTML, CSS and Javascript files included with the template in your favorite text editor to make changes. These are the only files you need to worry about, you can ignore everything else! To preview the changes you make to the code, you can open the `generateHTML.js` file in your web browser.

### Guidelines:

- Proceeds as follows:

The user will be prompted for a **GitHub Username** and **favorite color**, which will be used as the background color for cards.

The PDF will be populated with the following:

- Profile image
- User name
- Links to the following:
  - User location via Google Maps
  - User GitHub profile
  - User blog
- User bio
- Number of public repositories
- Number of followers
- Number of GitHub stars
- Number of users following

### Code Snippet

```javascript
-index.js check point

...
// setup axios config to get data from github api
      const config = {
        headers: {
          accept: 'application/json'
        }
// Get GitHub API data by the axios get method
      let queryUrl = `https://api.github.com/users/${username}`;

      return axios.get(queryUrl, config).then(userData => {
        let newUrl = `https://api.github.com/users/${username}/starred`;

...
// function to create index.html file using generateHTML.js
const creatHTML = function(generateHTML) {
  writeFileAsync('index.html', generateHTML);
};

// generatePDF Funcion puppeteer accoding to puppeteer guide line
async function generatePDF(username) {
  try {
    const browser = await puppeteer.launch();
    const page = await browser.newPage();

    // setup index.html file location
    await page.goto(
      'file:///Users/esjung/BootcampBK/homeworks/Developer-Profile-Generator/index.html'
    );
    await page.emulateMediaType('screen');

    // setup puppeteer pdf generation options
    await page.pdf({
      path: `${username}.pdf`,
      format: 'Letter',
      printBackground: true,
      landscape: true
    });
    console.log('Generated PDF sucessfully !');

    await browser.close();
  } catch (err) {
    console.log('Oops! PDF generate error !!!');
  }
}

```

## Built With

- [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [puppeteer.js](https://developers.google.com/web/tools/puppeteer)

## Authors

- **Michael(Eunsoo)Jung**

* [Developer Profile Generator: Node.js and ES6](https://eunsoojung.github.io/Developer-Profile-Generator/)
* [My Portfolio](https://eunsoojung.github.io/Unit-02-Responsive-Portfolio/portfolio.html)
* [Link to Github](https://github.com/)
* [Link to LinkedIn](www.linkedin.com/in/eun-soo-jung/)

## License

This project is licensed under the MIT License
