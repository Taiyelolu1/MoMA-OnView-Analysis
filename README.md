# MoMA OnView Analysis
This research dataset contains 157,630 records, representing all of the works that have been accessioned into MoMA’s collection and cataloged in their database. It includes basic metadata for each work, including title, artist, date made, medium, dimensions, and date acquired by the Museum. This project focuses on the artworks currently on display at the museum (MoMA OnView). The dataset used for this project was sourced from [Maven Analytics Playground](https://mavenanalytics.io/data-playground).
## Project Bacground
The Museum of Modern Art (MoMA) is an art museum located in Midtown Manhattan, New York City, on 53rd Street between Fifth and Sixth Avenues. MoMA's collection spans the late 19th century to the present, and includes over 200,000 works of architecture and design, drawing, painting, sculpture, photography, prints, illustrated and artist's books, film, as well as electronic media.

The museum has been instrumental in shaping the history of modern art, particularly modern art from Europe. In recent decades, MoMA has expanded its collection and programming to include works by traditionally underrepresented groups. The MoMA Library includes about 300,000 books and exhibition catalogs, more than 1,000 periodical titles and more than 40,000 files of ephemera about individual artists and groups. The archives hold primary source material related to the history of modern and contemporary art. In 2023, MoMA was visited by over 2.8 million people, making it the 15th most-visited art museum in the world and the 6th most-visited museum in the United States.

## Overview of the Data
The data contained two tables; Artists and Artworks. The data was `cleaned` and `transformed` using the `Power Query Editor` in Power BI. The major transformations carried out in the Power Query Editor inlcude:
* Removal of unwanted columns: Columns that were found to be unuseful for the analysis were removed so as to focus on the ones needed.
* Renaming Columns: Some columns were also renamed for easy understanding in the course of the project.
* Replacing values: Columns with blank rows were replaced with "Unknown" or "null".
* Formatting columns: Records in the columns were given proper data types, trimmed, and given proper casing to give a better uniform look of the tables.
* Added column: Added a custom column `Year` by extracting the first four digit from the `Date` column.

After cleaning, the columns left in both tables include:

**Artists**
* ConstituentID: A unique identifier for the artist in the museum's database system.
* ArtistName: The public display name of the artist, which may be their full name, pseudonym, or stage name.
* ArtistBio: A short biography or background information about the artist. 
* Nationality: The country or region the artist is originally from. 
* Gender: The gender of the artist.
* BirthDate: The birth year of the artist.
* DeathDate: The death year of the artist.

**Artworks**
* ObjectID: A unique identifier for the artwork in the MoMA database system.
* Title: The name or title of the artwork
* ConstituentID: Unique identifier(s) for the artist(s) related to the artwork (separated by commas).
* Year: Year the artwork was created. 
* Medium: The material(s) used to create the artwork, such as oil paint, marble, video or other mediums.
* Dimensions: The size or physical dimensions of the artwork (e.g., height x width x depth in cm).
* Classification: The classification of the artwork, such as painting, sculpture, drawing, photography etc.
* Department: The department of the museum where the artwork is stored or categorized. 
* DateAquired: The date the artwork was acquired by the museum. 
* URL: A web link to more detailed information about the artwork on the MoMA website. 
* ImageURL: The URL of the image of the artwork, hostedby the museum. 
* OnView: Location of the artwork if it is currently on display in the museum (otherwise blank).

***The CSV files and scripts generated from the Power Query Editor have been included in the repository for this project.***

## Tools used 
1. **Power BI**: This was the major tool used in this project. Power BI was used in creating the `visualization` and report for the insights generated from this project. Power BI service, a component of Power BI was also utilized in creating a web link that allows interactivity and navigation with the report.
2. **Power Query Editor**: This is an advanced feature of Power BI that allows transformation to be carried out on a dataset. The `Power Query Editor` was used in carrying out transformations across different columns such as adding custom columns, formatting columns, replacing values, etc.

## Project Workflow
A Project Workflow provides a good structure for every data analytics project. It helps to establish a clear roadmap of sequential steps from the initial problem to the final insights. This keeps the project organized and aligned with goals. It also outlines tasks within each project phase, preventing important elements from being overlooked and making the process more efficient. The workflow for this project includes:
1. Project objective.
2. Data collection.
3. Data cleaning and preparation.
4. Data analysis and visualization.
5. Interpretation and reporting.

## Project Objective
This project was aimed at focusing on the analysis of artworks which are currently in display at MoMa. Insights about the artists featured, the number of artworks they have done, the types of artworks in the museum etc., can be gotten from this analysis. Power BI was used to provide interactive dashboards that support data-driven insights and strategic decision-making.

## Data Collection 
The data for this project was collected from [Maven Analytics Playground](https://mavenanalytics.io/data-playground). The data included records of various artists, their artworks, date of aquisition by the museum and much more. 
## Data Cleaning & Preparation
The data cleaning process was done using the Power Query Editor in Power BI. Some major operations such as removal of unwanted columns were done and other text operations such as capitalising, trimming, and replacing values were also carried out on some columns. The [M Query Codes] from the Power Query Editor have been attached to this repository. Please note that the Power Query Editor automatically writes/generates these codes based on the steps applied in the editor.

After data cleaning, a new column `Year` was created by extracting the first four (4) digits from the `Date` column. I made sure `Date` was first in the text datatype to make the extraction possible. Another major step taken was creating a bridge table `ArtworkArtists` so that each artist-arwork pairing has its own row. The various steps taken to achieve this include:

* Duplicated the `Artworks` table, keeping only columns; `ObjectID`, `Title`, `ConstituentID`, `Year` and `DateAquired`.
* Reordered the columns and change the table name to `ArtworkArtists`.
* Splitted the `ConstituentID` column by delimiter comma (,) into rows and changed the datatype to whole number.  

These were all done in the Power Query Editor. 

Outside Power Query Editor, a `DateTable` was created using the minimum and maximum date from the `DateAquired`. The table contained columns for `Date`, `year`, `Month`, `Month Number`, and `Quarter`. This table was marked as the date table. 

New relationships were created between the tables. These include:

* DateTable[Date] and Artworks[DateAquired].
* ArtworkArtists[ObjectID] and Artworks[ObjectID].
* ArtworkArtists[ConstituentID] and Artists[ConstituentID]. 

In addition, I created new measures and new columns (for different tables) to provide in-depth insights into the various records. Some of these measures and columns include:

**Artworks Table**
* **ArtistName(s)**: This column was created to show all the names of the artists that collaborated on the artworks. This was done by filtering from the `ArtworkArtists` table using the `ObjectID`.
* **CollaborationNumber**: This column was created to show the number of artists that collaborated on each artwork.

**Measures**
* **Total Artists**: This counts the total number of artists.
*  **Total Artworks**: This counts the total number of artworks on display in the museum.
*  **Most Prolific Artist**: This shows the artist with the highest number of artworks on display in the museum or the highest numberof collaborations.
*  **Most Recent Acquisition**: This shows the artwork that was last acquired by the museum.
*  **Oldest Artwork**: This shows the earliest artwork which was acquired by the museum.

Other tables were further created to help wih the analysis. These include:

* **CountryList**: This table had the list of all the nationalities of the artists with their corresponding countries. The data category for the country column was changed to `Country/Region`. A relationship was the created between the CountryList[Nationality] and Artists[Nationality].
* **ArtistImage**: This table was created with the top artists in mind. It had the ArtistName and the Image URL of the artists listed. This table was meant to be used as a tooltip. The data category for the Image URL column was changed to `Image URL`. A relationship was created between ArtistImage[ArtistName] and Artists[ArtistName].

Click [here] to view the `DAX functions` used to create the `measures`, `calculated columns`, and `Datetable`.

## Data Model
I created relationships between multiple tables. These include:

* DateTable[Date] and Artworks[DateAquired].
* ArtworkArtists[ObjectID] and Artworks[ObjectID].
* ArtworkArtists[ConstituentID] and Artists[ConstituentID].
* CountryList[Nationality] and Artists[Nationality].
* ArtistImage[ArtistName] and Artists[ArtistName].

![Data Model for MoMA OnView](https://github.com/user-attachments/assets/d1ba840a-4826-4c73-8bc7-aeef2ea0b56c)


## Data Analysis & Visualization
After cleaning and prepping the data, I began with my analysis and visualization. The visualization was divided into five (5) report pages for easy navigation and clarity of analysis. These reports were used to effectively visualize key insights from this analysis.

Some Key Insights from the data visualization are summarized below:

1. **Overview**: This section gives an overwiew of the whole data.
   * There were a total of **661** artists.
   * There were a total of **1,142** artworks on display in MoMA. 
   * The most prolific artist (artist with the highest amount of artwork done) was **Robert Frank**.
   * The most recently acquired artwork was **Veleuro**.
   * The year with the **highest number of acquired artworks** was **1934** with a total of 46 artworks acquired in that year.
   * The years **1932, 1962, 1987 and 1993** remain the years with the **least number of acquired artworks**.

   ![MoMA OnView-1](https://github.com/user-attachments/assets/151ae75c-a1ed-4456-9fba-1e2c1ac6a6c6)


2. **Artwork Info**: This section gives information about the Artworks. This covers the ObjectID, Title, ArtistName(s), Year, DateAquired and OnView (location in MoMA) of the artworks. It shows the picture of the artwork when a title is selected or when hovering on the table. There is also a search bar to narrow the search by Title or ArtistName(s).
   * Most recent acquired artwork is **Veleuro**.
   * Oldest artwork is **Self-Portrait with Palette**.

![MoMA OnView-2](https://github.com/user-attachments/assets/a381cd05-38f6-4f84-a2fa-6f9cea506818)


3. **Artwork Breakdown**: This section gives the distribution of the atworks based on different categories.
   * Top 5 Artworks by Classification include; Painting, Photograph, Drawing, Sculpture and Design.
   * Top 5 Artworks by Medium include; Oil on canvas, Gelatin silver print, Casein tempera on hardboard, Bronze and Gelatin silver print, printed 1997.
   * Total Artworks by Department was; Painting & Sculpture (39.84%), Drawing & prints (23.12%), Photography (19.7%), Architecture & Design (15.5%), Media & performance (1.66%) and Film (0.18).
   It also shows the distribution of artowrks in various locations of the museum in a table.

![MoMA OnView-3](https://github.com/user-attachments/assets/e31e3eb6-ab41-494f-94c8-32c419ac9f7d)


4. **Artist Breakdown**: This section shows the distribution of artists based on diffferent categories.
   * The map visual showing Total Artists by Country shows the number of artists in the countries based on gradient colours (the darker the colour, the higher the number). The country with the highest number of artists was United states of America with a total of 295 artists.
   * The distibution of Artists by Gender was; Male (64.9%), Female (28.9%), Unknown (6.05%) and Transgender woman (0.15).
   * Top 5 Artists by Artwork count were Robert Frank (55), Henri Matisse (38), Pablo Picasso (34), Jacob Lawrence (31), and Unidentified photographer (29).

   ***There is a tooltip applied to the Bar Chart showing Top 5 Artists by Artwork Count. This tooltip allows you see the image of the Artists when you hover on the chart***.

![MoMA OnView-4](https://github.com/user-attachments/assets/d1bd6f8a-b05c-4ac7-b62a-a77a812d00f3)


5. **Artist Info**: This sections shows a table representing information about the various artists. These include: ArtistName, Country, Gender, BirthYear, DeathYear and Artwork Count.

![MoMA OnView-5](https://github.com/user-attachments/assets/a445844a-474a-4746-89d1-f2ab63deba58)


 






