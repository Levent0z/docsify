# JAVA: Reading from Resource File

```java
package com.example.test;

public class Item {
    public String text;
    public boolean flag;
}
```

```java
package com.example.test.rest;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.example.test.Item;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.client.HttpServerErrorException;

import java.io.*;

@CrossOrigin
@RestController
@RequestMapping("test")
public class TestController {
    private static final Logger logger = LoggerFactory.getLogger(TestController.class);
    private Item[] items;

    public TestController() {
        try {
            this.items = ReadFile();
        } catch (Exception e) {
            logger.error(e.toString());
        }
    }

    public GateModel[] ReadFile() throws IOException {
        ObjectMapper objectMapper = new ObjectMapper();
        Item[] items;

        InputStream ins = getClass().getResourceAsStream("/items.json");
        try (BufferedReader reader = new BufferedReader(new InputStreamReader(ins))) {
            items = objectMapper.readValue(reader, Item[].class);
        }

        return items;
    }

    @GetMapping("items")
    public Item[] info() {
        if (this.items == null) {
            throw new HttpServerErrorException(HttpStatus.INTERNAL_SERVER_ERROR);
        }

        return this.items;
    }
}
```

Old Alternative:
```Java
// This piece of code works in IDE but not in a JAR.
File file = new File(getClass().getClassLoader().getResource("items.json").getFile());
byte[] jsonData = Files.readAllBytes(Paths.get(file.getPath()));
Item[] items = objectMapper.readValue(jsonData, Item[].class);
```
