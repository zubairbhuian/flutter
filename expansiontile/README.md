# ExpansionTile

**Copy the code here**
```dart

    ExpansionTile(
        title: Text("Zubair"),
        subtitle: Text("Fontend Developer"),
        // trailing: Icon(Icons.arrow_back_ios_sharp)
        leading: Icon(Icons.person_add_alt_sharp),
        children: [
        Container(
            height: 100,
            color: Colors.grey,
            child: ListView(children: [
            ListTile(
                title: Text("Demo text"),
                subtitle: Text("Here is some demo text"),
                trailing: Icon(Icons.add),
                onTap: () {},
            )
            ]),
        )
        ],
    )
 
 ```

> [SRC](https://github.com/zubairbhuian/flutter_test_one/tree/afran_42)