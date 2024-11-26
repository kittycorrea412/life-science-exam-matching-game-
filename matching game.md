<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Matching Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        .container {
            display: flex;
            justify-content: space-between;
        }
        .column {
            width: 45%;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
        li {
            margin: 10px 0;
            padding: 10px;
            border: 1px solid #ccc;
            cursor: pointer;
        }
        .matched {
            background-color: #d4edda;
            border-color: #c3e6cb;
            pointer-events: none;
        }
    </style>
</head>
<body>
    <h1>Interactive Matching Game</h1>
    <p>Drag items from Column A to match with Column B!</p>
    <div class="container">
        <div class="column" id="columnA">
            <h2>Column A</h2>
            <ul>
                <li draggable="true" id="1">Mitosis</li>
                <li draggable="true" id="2">Meiosis</li>
                <li draggable="true" id="3">Tetrads</li>
                <li draggable="true" id="4">Karyotype</li>
                <li draggable="true" id="5">Autosomes</li>
            </ul>
        </div>
        <div class="column" id="columnB">
            <h2>Column B</h2>
            <ul>
                <li id="e">Produces genetically identical cells for growth and repair</li>
                <li id="k">Produces four haploid cells for sexual reproduction</li>
                <li id="i">Pair of homologous chromosomes formed during Prophase I</li>
                <li id="o">Pictorial representation of chromosomes</li>
                <li id="f">Chromosomes not involved in determining sex</li>
            </ul>
        </div>
    </div>
    <script>
        const items = document.querySelectorAll('[draggable]');
        const matches = {
            1: 'e',
            2: 'k',
            3: 'i',
            4: 'o',
            5: 'f'
        };

        items.forEach(item => {
            item.addEventListener('dragstart', dragStart);
        });

        document.querySelectorAll('#columnB li').forEach(target => {
            target.addEventListener('dragover', dragOver);
            target.addEventListener('drop', drop);
        });

        function dragStart(event) {
            event.dataTransfer.setData('text/plain', event.target.id);
        }

        function dragOver(event) {
            event.preventDefault();
        }

        function drop(event) {
            event.preventDefault();
            const draggedId = event.dataTransfer.getData('text/plain');
            const targetId = event.target.id;

            if (matches[draggedId] === targetId) {
                const draggedItem = document.getElementById(draggedId);
                draggedItem.classList.add('matched');
                event.target.classList.add('matched');
                event.target.innerHTML += ` <strong>(${draggedItem.textContent})</strong>`;
                draggedItem.draggable = false;
            }
        }
    </script>
</body>
</html>
