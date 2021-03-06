# Instruction for creating new page

## **Step 1:** Setting up your system environment

First install latest “Node.js” version for your windows PC from [here](https://nodejs.org/en/download/).

Now check, it installed or not.

Run the command

> node -v

You will see the latest node version like this

> v16.15.1

Open a new terminal and nevigate to the project directory.

> cd reliance-v2

And run the following command:

> npm install

Wait for it to be completed, it usually takes 5-10 minutes(or less) to complete.

## Start Development Server

Run the command

> npm start

**Note:** You must keep the development server running in a seperate terminal as long as you are performing any react native development tasks.
You need to keep this open in case of running or building the app from command line tools.

> You will see a link like this: http://localhost:8000/ in your terminal

> open this link in your browser and your will see your project live in your browser.

## **Step 2:** Adding new page

First download Visual studio code from [here](https://code.visualstudio.com/download) in your PC.

Open your project file in Visual Studio Code.

Then you will find a “src” folder in your project file

> src
> <img src="./img/src.png" alt="#"/>

**Then you will find a folder named “pages” in “src” folder**

> pages
> <img src="./img/pages.png" alt="#"/>

**Open it, and you will find a bunch of files. All these files are the files of pages of your website. Then you will find a file, named “samplePage.jsx”, which is your desired file for creating a new page.**

<img src="./img/samplePage.png" alt="#"/>

**Now create a copy of the “samplePage.jsx” in pages folder and rename it as your new page name like “newPage.jsx”**

```html
/* eslint-disable react/prop-types */
import { graphql } from "gatsby";
import { Container } from "react-bootstrap";
import Layout from "@layout";
import { normalizedData } from "@utils/functions";
import { useEffect, useState } from "react";
import Preload from "../components/preloadPage/preload";
import Image from "./../data/images/blog/Engi@4x.png";

1: const SamplePage = ({ data }) => {
    const [preload, setPreload] = useState(true);
    const globalContent = normalizedData(data?.allGeneral?.nodes || []);

    useEffect(() => {
        setPreload(false);
    }, []);

    return (
        <Layout
            data={{
                ...globalContent["menu"],
                ...globalContent["footer"],
            }}
        >
            {" "}
            {preload && <Preload />}
            <Container>
                {/* You can start code here */}

                <h1 style={{ textAlign: "center" }}>This is your heading</h1>
                <p style={{ textAlign: "center" }}>This is your paragraph</p>
                <img src={Image} alt='#' style={{ marginBottom: "20px" }} />
            </Container>
        </Layout>
    );
};

export const query = graphql`
2:    query SamplePageQuery {
        allGeneral {
            nodes {
                section
                id
                menu {
                    ...Menu
                }
                footer {
                    ...Footer
                }
            }
        }
        allArticle {
            nodes {
                ...Articles
            }
        }
    }
`;

3: export default SamplePage;

```

> **Note:** Rename three places in the file as your page name, where 1, 2, 3 number are located, on those lines.

Now your new page is ready to see.

open your browser and type in URL

> http://localhost:8000/newPage

And you will see the new page with a heading, a paragraph and an image.

Now you can coustomize this page as you want by coading in the container tag.

```html
<Container>
    {/* You can start code here */}

    <h1 style={{ textAlign: "center" }}>This is your  	heading</h1>
    <p style={{ textAlign: "center" }}>This is your paragraph</p>
    <img src={Image} alt='#' style={{ marginBottom: "20px" }} />
</Container>
```

> **Note:** In this similiar way you can create any page in your website. Such as: you can copy "Board of director" page in 'about' folder and do the same operation on that file, then coustomize it

## **Step 3:** Adding the new page link to the menu

You will find a folder named "data" in the "src" folder. Open it, and there is a "generel" folder in that "data" folder

<img src="./img/menu.png" alt="#"/>

In that "general" folder you will find json data file "menu.json" and "footer.json". Now you can add this new page link any where in these "menu.json" and "footer.json" data files.

### **An example is provided for understanding adding link to menu.**

>     	{
>            "id": "menu-6",
>            "text": "Info",
>           "link": "/",
>           "submenu": [
>                {
>                   "id": "menu-61",
>                   "text": "Agent info",
>                   "link": "/info/agent-info"
>                },
>                {
>                    "id": "menu-62",
>                    "text": "BOD Executives",
>                    "link": "/info/bod-executives"
>                },
>                {
>                    "id": "menu-63",
>                    "text": "Claim Info",
>                    "link": "/info/claim-info"
>                }
>           ]
>        },

In menu.json file, you will find an object with "id": "menu-6", there is "submenu" property in that object, which is an array of three object.

> **Note:** array enclosed in [] , and object enclosed in {} .

Now add forth object in "submenu" array and save this.

>     	{
>            "id": "menu-6",
>            "text": "Info",
>            "link": "/",
>            "submenu": [
>                {
>                    "id": "menu-61",
>                    "text": "Agent info",
>                    "link": "/info/agent-info"
>                },
>                {
>                    "id": "menu-62",
>                    "text": "BOD Executives",
>                    "link": "/info/bod-executives"
>                },
>                {
>                    "id": "menu-63",
>                    "text": "Claim Info",
>                    "link": "/info/claim-info"
>                },
>                {
>                    "id": "menu-64",
>                    "text": "New Page",
>                    "link": "/newPage"
>                }
>            ]
>        },

In this format,

=> "id" is the key identification of that item. And it must be unique for every item.

> "id": "menu-64",

=> "text" is the name of the menu item.

> "text": "New Page",

=> "link" is the page route link. Which we discussed earlier.

> "link": "/newPage"

### **An example is provided for understanding adding link to footer.**

Go to "footer.json" file and edit

        {
            "id": "footer-3",
            "title": "About Us",
            "list": [
                {
                    "id": "footer-list-31",
                    "text": "Company Profile",
                    "link": "/about/about-us"
                },
                {
                    "id": "footer-list-32",
                    "text": "Chairman's Profile",
                    "link": "/about/chairman's-profile"
                },
                {
                    "id": "footer-list-33",
                    "text": "Chief Consultant's Profile",
                    "link": "/about/chief-consultant's-profile"
                },
                {
                    "id": "footer-list-34",
                    "text": "CEO's Profile",
                    "link": "/about/ceo's-profile"
                },
                {
                    "id": "footer-list-35",
                    "text": "Board Of Directors",
                    "link": "/about/board-of-directors"
                },
                {
                    "id": "footer-list-36",
                    "text": "Management",
                    "link": "/about/management"
                },
                {
                    "id": "footer-list-37",
                    "text": "Divisions-Depts",
                    "link": "/about/divisions-depts"
                },
                {
                    "id": "footer-list-38",
                    "text": "Organogram",
                    "link": "/about/organogram"
                }
            ]
        },

Now add the below object in "submenu" array as you saw in the previous example.

       {
                    "id": "footer-list-38",
                    "text": "New Page",
                    "link": "/newPage"
                }

Now you will see the last added item in footer about menu list.

# Creating a product page:

> Copy any product page and rename it as your new product with extention '.jsx'.

```html
import PropTypes from "prop-types";
import { graphql } from "gatsby";
import { Container } from "react-bootstrap";
import Layout from "@layout";
import SEO from "@components/seo";
import { normalizedData } from "@utils/functions";
import jsonDataInit from "../../data/products/engineering-insurance.json";
import axios from "axios";
import { useEffect, useState } from "react";
import Preload from "../../components/preloadPage/preload";


1. const Engineering = ({ data, location, pageContext }) => {
    const [jsonData, setJsonData] = useState(jsonDataInit);
    const [preload, setPreload] = useState(true);
    useEffect(() => {
        axios(
            "https://reliance-admin.dev.quanticdynamics.cloud/api/sendJSON/62a7312178fc357870f08ff7"
        )
            .then((resultData) => {
                setJsonData(resultData.data);
                setPreload(false);
            })
            .catch((err) => {
                console.log(err);
                setPreload(false);
            });
    }, []);
    const globalContent = normalizedData(data?.allGeneral?.nodes || []);
    return (
        <Layout
            data={{
                ...globalContent["menu"],
                ...globalContent["footer"],
            }}
        >
            {" "}
            {preload && <Preload />}
            <SEO title="Engineering Insurance" pathname="/" />
            <Container>
                <img
                    style={{
                        marginTop: "10px",
                        marginBottom: "30px",
                        borderRadius: "10px",
                    }}
                    src={jsonData[0].image}
                    alt="Engineering"
                />
                <div
                    style={{
                        marginBottom: "30px",
                    }}
                >
                    <h3>{jsonData[0].title}</h3>
                    <ul>
                        <li
                            style={{
                                fontSize: "17px",
                                marginLeft: "20px",
                                color: "#000",
                            }}
                        >
                            {jsonData[0].title1}
                        </li>
                        <li
                            style={{
                                fontSize: "17px",
                                marginLeft: "20px",
                                color: "#000",
                            }}
                        >
                            {jsonData[0].title2}
                        </li>
                        <li
                            style={{
                                fontSize: "17px",
                                marginLeft: "20px",
                                color: "#000",
                            }}
                        >
                            {jsonData[0].text}
                        </li>
                        <li
                            style={{
                                fontSize: "17px",
                                marginLeft: "20px",
                                color: "#000",
                            }}
                        >
                            {jsonData[0].text1}
                        </li>
                        <li
                            style={{
                                fontSize: "17px",
                                marginLeft: "20px",
                                color: "#000",
                            }}
                        >
                            {jsonData[0].text2}
                        </li>
                        <li
                            style={{
                                fontSize: "17px",
                                marginLeft: "20px",
                                color: "#000",
                            }}
                        >
                            {jsonData[1].title2}
                        </li>
                        <li
                            style={{
                                fontSize: "17px",
                                marginLeft: "20px",
                                color: "#000",
                            }}
                        >
                            {jsonData[1].title1}
                        </li>
                        <li
                            style={{
                                fontSize: "17px",
                                marginLeft: "20px",
                                color: "#000",
                            }}
                        >
                            {jsonData[1].title2}
                        </li>
                        <li
                            style={{
                                fontSize: "17px",
                                marginLeft: "20px",
                                color: "#000",
                            }}
                        >
                            {jsonData[1].text}
                        </li>
                        <li
                            style={{
                                fontSize: "17px",
                                marginLeft: "20px",
                                color: "#000",
                            }}
                        >
                            {jsonData[1].text1}
                        </li>
                    </ul>
                    <p style={{ color: "#000", fontSize: "18px" }}>
                        {jsonData[1].text2}
                    </p>
                </div>
            </Container>
        </Layout>
    );
};
2. Engineering.propTypes = {
    location: PropTypes.object,
    pageContext: PropTypes.object,
    data: PropTypes.shape({
        allGeneral: PropTypes.shape({
            nodes: PropTypes.arrayOf(PropTypes.shape({})),
        }),
        allArticle: PropTypes.shape({
            nodes: PropTypes.arrayOf(PropTypes.shape({})),
        }),
    }),
};

export const query = graphql`
3.    query EngineeringQuery {
        allGeneral {
            nodes {
                section
                id
                menu {
                    ...Menu
                }
                footer {
                    ...Footer
                }
            }
        }
        allArticle {
            nodes {
                ...Articles
            }
        }
    }
`;

4. export default Engineering;

```

> **Note:** Rename four places in the file as your page name, where 1, 2, 3, 4 number are located, on those lines.

At first change the product page image

```html
<img style={{ marginTop: "10px", marginBottom: "30px", borderRadius: "10px", }}
src={jsonData[0].image} alt="Engineering" />
```

Then if you need heading, add a heading tag.

```html
<h1>Paste your heading here</h1>
```

If you need paragraph, add a paragraph tag.

```html
<p>Paste your paragraph here</p>
```

In this way you can costomize the new product page by adding tags.

> **Note:** You can create any new similiar pages by following above procedure.
