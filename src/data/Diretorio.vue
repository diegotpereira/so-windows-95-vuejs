<script>
export default [
    [
        "Meu Computador",
        "MyComputer",
        "Pasta",
        true,
        [
            ["3½ Floppy (A:)", "FloppyDrive", "Pasta", true],
            [
                "Disco Local (C:)",
                "Drive",
                "Pasta",
                true,
                [
                    ["Meus Documentos", "MyDocuments", "Pasta", true],
                    ["Minhas Fotos", "Folder", "Pasta", true],
                ],
            ],
            ["(D:)", "DiskDrive", "Pasta", true],
            ["Painel de Controle", "Folder", "Pasta", true],
        ],
    ],
    ["Internet", "Internet", "Internet", true],
    ["Bloco de Notas", "Notepad", "BlocoNotas", true],
    ["Paint", "Paint", "Paint", true],
    ["Programas", "Programs", "Pasta", true,
    [
        ["Internet", "Internet", "Internet", true],
        ["Bloco de Notas", "Notepad", "BlocoNotas", true],
        ["AOL", "AOL", "AOL", true],
        ["Paint", "Paint", "Paint", true],
    ],
    ],
    ["Lixeira", "RecycleBin", "Pasta", true],
    ["Pasta", "Folder", "Pasta", true,
       [
        [
            "Jogos", "Folder", "Pasta", true,
            [
                ["Exemplo", "Internet", "Internet", true],
                ["OctoPet", "Internet", "Internet", true],
                ["Even Deeper Folder", "Folder", "Pasta", true,
                   [["Lixeira", "RecycleBin", "Pasta", true]],
                ],
            ],
        ],
        ["Internet Link", "Internet", "Internet", true],
       ],
    ],
];
</script>