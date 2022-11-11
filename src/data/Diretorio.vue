<script>
export default [
    [
        "Meu Computador",
        "MyComputer",
        "Folder",
        true,
        [
            ["3½ Floppy (A:)", "FloppyDrive", "Folder", true],
            [
                "Disco Local (C:)",
                "Drive",
                "Folder",
                true,
                [
                    ["Meus Documentos", "MyDocuments", "Folder", true],
                    ["Minhas Fotos", "Folder", "Folder", true]
                ]
            ],
            ["(D:)", "DiskDrive", "Folder", true],
            ["Painel de Controle", "Folder", "Folder", true],
        ]
    ],
    ["Internet", "Internet", "Internet", true],
    ["Bloco de Notas", "Notepad", "Notepad", true],
    ["Paint", "Paint", "Paint", true],
    ["Programas", "Programs", "Folder", true,
    [
        ["Internet", "Internet", "Internet", true],
        ["Notepad", "Notepad", "Notepad", true],
        ["AOL", "AOL", "AOL", true],
        ["Paint", "Paint", "Paint", true]
    ]
    ],
    ["Lixeira", "RecycleBin", "Folder", true],
    ["Pasta", "Folder", "Folder", true,
       [
        [
            "Jogos", "Folder", "Folder", true,
            [
                ["Exemplo", "Internet", "Internet", true],
                ["OctoPet", "Internet", "Internet", true],
                ["Even Deeper Folder", "Folder", "Folder", true,
                   [["Lixeira", "RecycleBin", "Folder", true]]
                ],
            ],
        ],
        ["Internet Link", "Internet", "Internet", true]
       ],
    ],
];
</script>