#how to load json file in a c# class

1. create a json file
    ```json
    {
        "prop":"value"
    }
    ```json
2. ceate a c# model class

    ```c#
    using Newtonsoft.Json;
    public Myclass{
        [JsonProperty("prop")]
        public string Prop {get;set;}

        public static Myclass LoadFromJsonFile(string filepath)
            {
                string data = File.ReadAllText(filepath);
                Myclass instance = JsonConvert.DeserializeObject<Myclass>(data);
                return instance;
            }
    }
    ```

>**Note:** Don't forget to copy your json file into build output directory in post build event
copy /y $(ProjectDir)\appsettings.json $(TargetDir)