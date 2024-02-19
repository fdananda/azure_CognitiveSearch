# Azure Cognitive Search

Projeto da aula Azure Cognitive Search

## Criando o recurso do Azure AI Search
1. Acessar o portal do Azure no endereço https://portal.azure.com;
2. Clique na opção + Create a resource;
3. Coloque na busca Azure Ai Search;
4. Selecione a opção Azure Ai Search;
5. Clique no botão Create;
6. Preencha o formulário com as informações a seguir:
- Subscription: Azure subscription 1
- Resource group: laboratorio_dio
- Service name: searchservic
- Location: East US
- Pricing tier: Basic (>>Select)
>> Review + create<br>
>> Create

## Criando um recurso de serviços de IA
7. Acessar o portal do Azure no endereço https://portal.azure.com;
8. Clique na opção + Create a resource;
9. Coloque na busca Azure Ai services;
10. Selecione a opção Azure Ai services;
11. . Clique no botão Create;
12. Preencha o formulário com as informações a seguir:
- Subscription: Azure subscription 1
- Resource group: laboratorio_dio
- Region: East US
- Name: servic
- Pricing tier: Standard S0
- By checking this box I acknowledge that I have read and understood all the terms below: selecionado
>> Review + create<br>
>> Create

## Criando uma conta de armazenamento
13. Acessar o portal do Azure no endereço https://portal.azure.com;
14. Clique na opção + Create a resource;
15. Coloque na busca Storage account;
16. Selecione a opção Storage account;
17. Clique no botão Create;
18. Preencha o formulário com as informações a seguir:
- Subscription: Azure subscription 1
- Resource group: laboratorio_dio
- Storage account name: classdiosa
- Region: (US )East US
- Performance: Standard
- Redundancy: Locally-redundant storage (LRS)
>> Review<br>
>> Create
19. Clique em Go to resource;
20. Clique em Configuration no menu lateral esquerdo;
21. Marque a opção Enabled abaixo da linha Allow Blob anonymous access;
>> Save
22. Selecione Containers;
23. Selecione + Container;
24. Preencha o formulário com as informações a seguir:
- Name: coffee-reviews
- Public access level: Container (anonymous read access for containers and blobs)
>> Create
25. Selecione a opção que foi criada;
26. Selecione Upload;
27. Selecione a opção Browse for files;
28. Selecione os arquivos;
29. Acessar o  recurso do Azure AI Search
30. Escolher a opção Import data;
31. Em Data Source, selecionar Azure Blob Storage e preencher o formulário:
- Data Source: Azure Blob Storage
- Data source name: coffee-customer-data
- Data to extract: Content and metadata
- Parsing mode: Default
- Connection string: Selecionar Choose an existing connection. Seleciuonar a storage account que havia sido criada e escolher coffee-reviews container e Select.
- Managed identity authentication: None
- Container name: coffee-reviews
- Blob folder: não preencher
- Description: Reviews for Fourth Coffee shops
>> Next: Add cognitive skills (Optional)
32. Na opção Attach AI Services, selecione servic;
33. Na opção Add enrichments, preencha: 
- Skillset name: coffee-skillset
-  Enable OCR and merge all text into merged_content field: selecionado
- Source data field: merged_content
- Enrichment granularity level: Pages (5000 character chunks)
- Enable incremental enrichment: não selecionado
- Selecionar as opções:<br> 
Extract location names	 	Extract key phrases
Detect sentiment
Generate tags from images	 	
Generate captions from 
34. Na opção Save enrichments to a knowledge store, marque todas as opções;
>> Next: Customize target index
35. Preencha o formulário com os dados:
- Index name: coffee-index
- Key: metadata_storage_path
- Suggester name: não preenchido
- Search mode: preenchimento automático
- Em content, marcar a opção Filterable
>>  Next: Create an indexer
36. Preencha o formulário:
- Name: coffee-indexer
- Schedule: Once
- Description: Não preenchido
- Base-64 Encode Keys: selecionado
>> Submit
37. Selecione Indexers;
38. Selecione o Index criado para mais detalhes;
39. Selecione a opção Search Explorer para fazer as consultas
40. Json obtido para a consulta "Chicago":
```
{
  "@odata.context": "https://searchservic.search.windows.net/indexes('coffee-index')/$metadata#docs(*)",
  "value": [
    {
      "@search.score": 5.0833344,
      "content": "\n\nReview: The coffee tastings every Wednesday afternoon are so fun. Each month there is a new drink theme. You do need to book a spot in advance to attend. It is very worth it! I also love their local music. Fourth Coffee brings in rising artists every weekend. I like to head over there mid-afternoon on weekdays when it’s not too busy and get a slice of pie or their seasonal baked goods.  \nDate: August 13, 2018\nLocation: Chicago, Illinois  \n\nimage1.png\n\n\n\nimage2.png\n\n\n\n",
      "metadata_storage_path": "aHR0cHM6Ly9jbGFzc2Rpb3NhLmJsb2IuY29yZS53aW5kb3dzLm5ldC9jb2ZmZWUtcmV2aWV3cy9yZXZpZXctNC5kb2N40",
      "locations": [
        "Fourth Coffee",
        "Chicago",
        "Illinois"
      ],
      "keyphrases": [
        "new drink theme",
        "seasonal baked goods",
        "coffee tastings",
        "local music",
        "Fourth Coffee",
        "rising artists",
        "ierican Coffee",
        "Review",
        "afternoon",
        "spot",
        "advance",
        "weekdays",
        "slice",
        "pie",
        "Date",
        "August",
        "Location",
        "Chicago",
        "Illinois"
      ],
      "sentiment": "[\"positive\"]",
      "merged_content": "\n\nReview: The coffee tastings every Wednesday afternoon are so fun. Each month there is a new drink theme. You do need to book a spot in advance to attend. It is very worth it! I also love their local music. Fourth Coffee brings in rising artists every weekend. I like to head over there mid-afternoon on weekdays when it’s not too busy and get a slice of pie or their seasonal baked goods.  \nDate: August 13, 2018\nLocation: Chicago, Illinois  \n\nimage1.png\n ierican Coffee 114 10148/0034 \n\n\nimage2.png\n  \n\n\n",
      "text": [
        "ierican Coffee 114 10148/0034",
        ""
      ],
      "layoutText": [
        "{\"language\":\"en\",\"text\":\"ierican Coffee 114 10148/0034\",\"lines\":[{\"boundingBox\":[{\"x\":701,\"y\":284},{\"x\":649,\"y\":303},{\"x\":647,\"y\":297},{\"x\":699,\"y\":279}],\"text\":\"ierican Coffee\"},{\"boundingBox\":[{\"x\":682,\"y\":241},{\"x\":614,\"y\":263},{\"x\":611,\"y\":251},{\"x\":678,\"y\":228}],\"text\":\"114 10148/0034\"}],\"words\":[{\"boundingBox\":[{\"x\":701,\"y\":285},{\"x\":679,\"y\":293},{\"x\":676,\"y\":287},{\"x\":699,\"y\":279}],\"text\":\"ierican\"},{\"boundingBox\":[{\"x\":676,\"y\":294},{\"x\":652,\"y\":303},{\"x\":650,\"y\":297},{\"x\":674,\"y\":288}],\"text\":\"Coffee\"},{\"boundingBox\":[{\"x\":682,\"y\":242},{\"x\":672,\"y\":245},{\"x\":668,\"y\":232},{\"x\":678,\"y\":229}],\"text\":\"114\"},{\"boundingBox\":[{\"x\":669,\"y\":245},{\"x\":618,\"y\":262},{\"x\":615,\"y\":251},{\"x\":666,\"y\":233}],\"text\":\"10148/0034\"}]}",
        "{\"language\":\"en\",\"text\":\"\",\"lines\":[],\"words\":[]}"
      ],
      "imageTags": [
        "food",
        "chocolate",
        "table",
        "cup",
        "serveware",
        "indoor",
        "cocoa solids",
        "caffeine",
        "tableware",
        "sitting",
        "coffee",
        "dessert",
        "musical instrument",
        "music",
        "concert",
        "clothing",
        "person",
        "string instrument",
        "human face",
        "microphone",
        "plucked string instruments",
        "acoustic guitar",
        "guitar",
        "indoor",
        "woman"
      ],
      "imageCaption": [
        "{\"tags\":[\"cup\",\"coffee\",\"table\",\"indoor\",\"pastry\",\"beverage\",\"breakfast\",\"close\"],\"captions\":[{\"text\":\"a group of small cups with brown liquid in them\",\"confidence\":0.39556038379669189}]}",
        "{\"tags\":[\"person\",\"music\",\"guitar\",\"bowed instrument\",\"bass\"],\"captions\":[{\"text\":\"a person playing a guitar\",\"confidence\":0.54444891214370728}]}"
      ]
    },
    {
      "@search.score": 1.0774994,
      "content": "\nReview: I often make Fourth Coffee my meeting spot for my client meetings weekday mornings. I own a small business and the folks who work at Fourth Coffee are always very friendly. It leaves a good impression on my clients. There are also plenty of drink selections, good wi-fi, and seating. Some of my favorite coffees are the lavender honey latte and, in the winter, the apple-chai latte. There are delicious baked goods offered as well. \nDate: October 21, 2018\nLocation: Chicago, Illinois \n\nimage1.png\n\n\n\n",
      "metadata_storage_path": "aHR0cHM6Ly9jbGFzc2Rpb3NhLmJsb2IuY29yZS53aW5kb3dzLm5ldC9jb2ZmZWUtcmV2aWV3cy9yZXZpZXctNS5kb2N40",
      "locations": [
        "meeting spot",
        "Chicago",
        "Illinois"
      ],
      "keyphrases": [
        "delicious baked goods",
        "lavender honey latte",
        "apple-chai latte",
        "Fourth Coffee",
        "meeting spot",
        "client meetings",
        "small business",
        "good impression",
        "drink selections",
        "good wi",
        "favorite coffees",
        "Review",
        "mornings",
        "folks",
        "clients",
        "plenty",
        "fi",
        "seating",
        "winter",
        "Date",
        "October",
        "Location",
        "Chicago",
        "Illinois"
      ],
      "sentiment": "[\"positive\"]",
      "merged_content": "\nReview: I often make Fourth Coffee my meeting spot for my client meetings weekday mornings. I own a small business and the folks who work at Fourth Coffee are always very friendly. It leaves a good impression on my clients. There are also plenty of drink selections, good wi-fi, and seating. Some of my favorite coffees are the lavender honey latte and, in the winter, the apple-chai latte. There are delicious baked goods offered as well. \nDate: October 21, 2018\nLocation: Chicago, Illinois \n\nimage1.png\n  \n\n\n",
      "text": [
        ""
      ],
      "layoutText": [
        "{\"language\":\"en\",\"text\":\"\",\"lines\":[],\"words\":[]}"
      ],
      "imageTags": [
        "clothing",
        "person",
        "furniture",
        "human face",
        "chair",
        "table",
        "woman",
        "indoor",
        "window",
        "desk",
        "sitting",
        "people",
        "restaurant"
      ],
      "imageCaption": [
        "{\"tags\":[\"person\",\"woman\",\"laptop\",\"dish\"],\"captions\":[{\"text\":\"a woman showing a woman something on a tablet\",\"confidence\":0.51351219415664673}]}"
      ]
    },
    {
      "@search.score": 0.96866095,
      "content": "Review: Today I was truly disappointed with how long I had to wait for the pastries I ordered ahead of time. When I got my box, some of the pastries seemed stale. Terrible experience!  \nDate: October 23, 2018\nLocation: Chicago, Illinois \n\n",
      "metadata_storage_path": "aHR0cHM6Ly9jbGFzc2Rpb3NhLmJsb2IuY29yZS53aW5kb3dzLm5ldC9jb2ZmZWUtcmV2aWV3cy9yZXZpZXctOC5kb2N40",
      "locations": [
        "Chicago",
        "Illinois"
      ],
      "keyphrases": [
        "Terrible experience",
        "Review",
        "pastries",
        "time",
        "box",
        "Date",
        "October",
        "Location",
        "Chicago",
        "Illinois"
      ],
      "sentiment": "[\"negative\"]",
      "merged_content": "Review: Today I was truly disappointed with how long I had to wait for the pastries I ordered ahead of time. When I got my box, some of the pastries seemed stale. Terrible experience!  \nDate: October 23, 2018\nLocation: Chicago, Illinois \n\n",
      "text": [],
      "layoutText": [],
      "imageTags": [],
      "imageCaption": []
    }
  ]
}
```

Ref.: documento criado como projeto em treinamento da Dio e com base na documentação oficial, disponível no endereço: https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html