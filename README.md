<!DOCTYPE html>
<html lang="da">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Storskrald Oversigt</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        h1, p { text-align: center; }
        p { font-size: 18px; }
    </style>
</head>
<body>
    <h1>Næste Storskraldsdato</h1>
    <p id="next-date">Indlæser...</p>
    <p id="next-address">Indlæser...</p>
    <script>
        const data = [
            { adresse: "Borgevej 25 B", by: "Lyngby", dato: "2025-02-21" },
            { adresse: "Sydtoftevej 11", by: "Søborg", dato: "2025-02-26" },
            { adresse: "Borgevej 25 B", by: "Lyngby", dato: "2025-03-21" },
            { adresse: "Sydtoftevej 11", by: "Søborg", dato: "2025-03-26" },
            { adresse: "Borgevej 25 B", by: "Lyngby", dato: "2025-04-18" },
            { adresse: "Sydtoftevej 11", by: "Søborg", dato: "2025-04-23" },
            { adresse: "Borgevej 25 B", by: "Lyngby", dato: "2025-05-16" },
            { adresse: "Sydtoftevej 11", by: "Søborg", dato: "2025-05-21" },
            { adresse: "Boligforeninger", by: "Farum + Værløse", dato: "2025-02-18" },
            { adresse: "Boligforeninger", by: "Farum + Værløse", dato: "2025-03-18" },
            { adresse: "Boligforeninger", by: "Farum + Værløse", dato: "2025-04-15" },
            { adresse: "Boligforeninger", by: "Farum + Værløse", dato: "2025-05-20" },
            { adresse: "Gladsaxevej 51", by: "Gladsaxe", dato: "2025-02-26" },
            { adresse: "Gladsaxevej 51", by: "Gladsaxe", dato: "2025-03-26" },
            { adresse: "Gladsaxevej 51", by: "Gladsaxe", dato: "2025-04-23" },
            { adresse: "Gladsaxevej 51", by: "Gladsaxe", dato: "2025-05-21" },
            { adresse: "Tulipanvej 5", by: "Vanløse", dato: "2025-04-03" },
            { adresse: "Søborg Hovedgade 12", by: "Søborg", dato: "2025-03-13" },
            { adresse: "Søborg Hovedgade 12", by: "Søborg", dato: "2025-04-10" },
            { adresse: "Søborg Hovedgade 12", by: "Søborg", dato: "2025-05-08" },
            { adresse: "Virumgårdsvej 2", by: "Virum", dato: "2025-02-20" },
            { adresse: "Virumgårdsvej 2", by: "Virum", dato: "2025-03-20" },
            { adresse: "Virumgårdsvej 2", by: "Virum", dato: "2025-04-17" },
            { adresse: "Virumgårdsvej 2", by: "Virum", dato: "2025-05-15" },
            { adresse: "Skovdiget 1", by: "Birkerød", dato: "2025-03-18" },
            { adresse: "Solvangsvej 7", by: "Glostrup", dato: "2025-03-24" },
            { adresse: "Solvangsvej 7", by: "Glostrup", dato: "2025-04-24" },
            { adresse: "Solvangsvej 7", by: "Glostrup", dato: "2025-05-21" },
            { adresse: "Solvangsvej 7", by: "Glostrup", dato: "2025-05-19" },
            { adresse: "Dorthesvej 35", by: "Holte", dato: "2025-03-04" },
            { adresse: "Landsevej 8A", by: "Holte", dato: "2025-03-11" },
            { adresse: "Landsebakken 24", by: "Holte", dato: "2025-03-11" },
            { adresse: "Lærkebakken 20", by: "Birkerød", dato: "2025-03-25" },
            { adresse: "Fyrrebakken 6", by: "Birkerød", dato: "2025-03-25" },
            { adresse: "Dronningsgård Alle 60", by: "Holte", dato: "2025-03-04" },
            { adresse: "Kollemosevej 7", by: "Holte", dato: "2025-03-04" },
            { adresse: "Skovalleen 33 B", by: "Bagsværd", dato: "2025-02-25" },
            { adresse: "Skovalleen 33 B", by: "Bagsværd", dato: "2025-03-25" },
            { adresse: "Skovalleen 33 B", by: "Bagsværd", dato: "2025-04-22" },
            { adresse: "Skovalleen 33 B", by: "Bagsværd", dato: "2025-05-20" },
            { adresse: "Bernhard Olsensvej 15", by: "Virum", dato: "2025-02-20" },
            { adresse: "Bernhard Olsensvej 15", by: "Virum", dato: "2025-03-20" },
            { adresse: "Bernhard Olsensvej 15", by: "Virum", dato: "2025-04-17" },
            { adresse: "Bernhard Olsensvej 15", by: "Virum", dato: "2025-05-15" }
        ];

        function findNextEntry(entries) {
            const today = new Date();
            const sortedEntries = entries.map(entry => ({
                ...entry,
                dateObj: new Date(entry.dato)
            })).sort((a, b) => a.dateObj - b.dateObj);

            for (let entry of sortedEntries) {
                if (entry.dateObj >= today) {
                    return entry;
                }
            }
            return null;
        }

        const nextEntry = findNextEntry(data);

        if (nextEntry) {
            document.getElementById("next-date").innerText = `Dato: ${nextEntry.dateObj.toLocaleDateString("da-DK")}`;
            document.getElementById("next-address").innerText = `Adresse: ${nextEntry.adresse}, ${nextEntry.by}`;
        } else {
            document.getElementById("next-date").innerText = "Ingen kommende datoer";
            document.getElementById("next-address").innerText = "";
        }
    </script>
</body>
