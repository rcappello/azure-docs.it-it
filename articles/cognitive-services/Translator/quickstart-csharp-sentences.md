---
title: 'Guida introduttiva: Ottenere la lunghezza delle frasi - API Traduzione testuale, C#'
titleSuffix: Azure Cognitive Services
description: In questa guida introduttiva si identifica la lunghezza delle frasi nel testo usando l'API Traduzione testuale con C#.
services: cognitive-services
author: noellelacharite
manager: cgronlun
ms.service: cognitive-services
ms.component: translator-text
ms.topic: quickstart
ms.date: 06/15/2018
ms.author: nolachar
ms.openlocfilehash: 699c4b775f2c5745a5b52593d44a0af408c5e73a
ms.sourcegitcommit: 74941e0d60dbfd5ab44395e1867b2171c4944dbe
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/15/2018
ms.locfileid: "49319608"
---
# <a name="quickstart-get-sentence-lengths-with-c35"></a>Guida introduttiva: Ottenere la lunghezza delle frasi con C#35;

In questa guida introduttiva si identifica la lunghezza delle frasi nel testo usando l'API Traduzione testuale.

## <a name="prerequisites"></a>Prerequisiti

Per eseguire questo codice in Windows, è necessario [Visual Studio 2017](https://www.visualstudio.com/downloads/). È possibile usare la versione gratuita Community Edition.

Per usare l'API Traduzione testuale, è necessario avere anche una chiave di sottoscrizione. Per informazioni, vedere [Come registrarsi all'API Traduzione testuale](translator-text-how-to-signup.md).

## <a name="breaksentence-request"></a>Richiesta di interruzione di frase

> [!TIP]
> Ottenere la versione più recente del codice da [GitHub](https://github.com/MicrosoftTranslator/Text-Translation-API-V3-C-Sharp).

Il codice seguente suddivide in frasi il testo di origine tramite il metodo [BreakSentence](./reference/v3-0-break-sentence.md).

1. Creare un nuovo progetto C# nell'ambiente di sviluppo integrato preferito.
2. Aggiungere il codice riportato di seguito.
3. Sostituire il valore di `key` con una chiave di accesso valida per la sottoscrizione.
4. Eseguire il programma.

```csharp
using System;
using System.Net.Http;
using System.Text;
// NOTE: Install the Newtonsoft.Json NuGet package.
using Newtonsoft.Json;

namespace TranslatorTextQuickStart
{
    class Program
    {
        static string host = "https://api.cognitive.microsofttranslator.com";
        static string path = "/breaksentence?api-version=3.0";

        static string uri = host + path;

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static string text = "How are you? I am fine. What did you do today?";

        async static void Break()
        {
            System.Object[] body = new System.Object[] { new { Text = text } };
            var requestBody = JsonConvert.SerializeObject(body);

            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Post;
                request.RequestUri = new Uri(uri);
                request.Content = new StringContent(requestBody, Encoding.UTF8, "application/json");
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);

                var response = await client.SendAsync(request);
                var responseBody = await response.Content.ReadAsStringAsync();
                var result = JsonConvert.SerializeObject(JsonConvert.DeserializeObject(responseBody), Formatting.Indented);

                Console.OutputEncoding = UnicodeEncoding.UTF8;
                Console.WriteLine(result);
            }
        }

        static void Main(string[] args)
        {
            Break();
            Console.ReadLine();
        }
    }
}
```

## <a name="breaksentence-response"></a>Risposta alla richiesta di interruzione di frase

Viene restituita una risposta con esito positivo in formato JSON, come illustrato nell'esempio seguente:

```json
[
  {
    "detectedLanguage": {
      "language": "en",
      "score": 1.0
    },
    "sentLen": [
      13,
      11,
      22
    ]
  }
]
```

## <a name="next-steps"></a>Passaggi successivi

Esaminare il codice di esempio per questa guida introduttiva e per altre, incluse quelle relative alla traduzione e alla traslitterazione, e anche altri progetti di esempio di Traduzione testuale su GitHub.

> [!div class="nextstepaction"]
> [Esaminare gli esempi di codice C# su GitHub](https://aka.ms/TranslatorGitHub?type=&language=c%23)
