# PokeGradeVirtualKit
<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pokémon Grading Calculator</title>
    <style>
        :root {
            --pk-yellow: #ffcb05;
            --pk-blue: #2a75bb;
            --bg: #1a1a1a;
            --card: #2d2d2d;
            --text: #ffffff;
        }

        body {
            font-family: 'Segoe UI', Roboto, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            display: flex;
            justify-content: center;
            padding: 20px;
        }

        .container {
            background: var(--card);
            padding: 2rem;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.5);
            width: 100%;
            max-width: 450px;
            border: 2px solid var(--pk-blue);
        }

        h2 { text-align: center; color: var(--pk-yellow); text-transform: uppercase; margin-bottom: 25px; }

        .grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }

        label { display: block; margin-bottom: 5px; font-size: 0.8rem; color: #aaa; }

        select {
            width: 100%;
            padding: 12px;
            background: #444;
            border: 1px solid #555;
            color: white;
            border-radius: 8px;
            font-size: 1rem;
            appearance: none; /* Rimuove freccia default */
        }

        .result-box {
            margin-top: 30px;
            text-align: center;
            background: linear-gradient(145deg, #333, #222);
            padding: 20px;
            border-radius: 15px;
            border: 1px solid var(--pk-yellow);
        }

        .grade-label { font-size: 0.9rem; color: var(--pk-yellow); font-weight: bold; }
        
        .grade-value { 
            font-size: 4rem; 
            font-weight: 900; 
            color: white; 
            display: block;
            text-shadow: 2px 2px 0px var(--pk-blue);
        }

        .info { font-size: 0.7rem; color: #777; margin-top: 15px; text-align: center; }
    </style>
</head>
<body>

<div class="container">
    <h2>Grading Simulator</h2>
    
    <div class="grid">
        <div>
            <label>Centratura</label>
            <select id="cent" onchange="calculateGrade()"></select>
        </div>
        <div>
            <label>Angoli</label>
            <select id="corn" onchange="calculateGrade()"></select>
        </div>
        <div>
            <label>Bordi</label>
            <select id="edge" onchange="calculateGrade()"></select>
        </div>
        <div>
            <label>Superficie</label>
            <select id="surf" onchange="calculateGrade()"></select>
        </div>
    </div>

    <div class="result-box">
        <span class="grade-label">VOTO FINALE STIMATO</span>
        <span class="grade-value" id="finalGrade">10</span>
    </div>

    <p class="info">Simulazione basata sulla media dei sub-grades.<br>Nessuna modifica permessa al calcolo.</p>
</div>

<script>
    // Popola i menu a tendina da 1 a 10 con incrementi di 0.5
    const selects = ['cent', 'corn', 'edge', 'surf'];
    selects.forEach(id => {
        const sel = document.getElementById(id);
        for(let i=10; i>=1; i-=0.5) {
            let opt = document.createElement('option');
            opt.value = i;
            opt.innerHTML = i;
            sel.appendChild(opt);
        }
    });

    function calculateGrade() {
        const v1 = parseFloat(document.getElementById('cent').value);
        const v2 = parseFloat(document.getElementById('corn').value);
        const v3 = parseFloat(document.getElementById('edge').value);
        const v4 = parseFloat(document.getElementById('surf').value);

        // Calcolo media semplice
        let media = (v1 + v2 + v3 + v4) / 4;

        // Arrotondamento tipico grading (al .0 o .5 più vicino per difetto)
        let finale = Math.floor(media * 2) / 2;

        // Visualizzazione
        document.getElementById('finalGrade').innerText = finale.toFixed(1);
    }
</script>

</body>
</html>
