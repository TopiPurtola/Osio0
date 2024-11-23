```mermaid
sequenceDiagram
    participant browser
    participant server

    %% Käyttäjä kirjoittaa uuden muistiinpanon ja painaa tallenna-nappia
    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    %% Palvelin käsittelee uuden muistiinpanon ja tallentaa sen
    server-->>browser: 200 OK (tieto on tallennettu)
    deactivate server

    %% Browser pyytää päivitystä uusilla muistiinpanoilla
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    %% Palvelin palauttaa kaikki muistiinpanot, mukaan lukien uusi
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server
    
    %% Selailu jatkuu, ja selain renderöi uuden muistiinpanon
    Note right of browser: The browser executes the callback function that renders the new note
