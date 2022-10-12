# check-box-list-
*Code main*
import 'package:listview_checkbox_secondtry/exports.dart';

class MainScreen extends StatefulWidget {
  const MainScreen({Key? key}) : super(key: key);

  @override
  State<MainScreen> createState() => _MainScreenState();
}

class _MainScreenState extends State<MainScreen> {
  List<Choice> choices = <Choice>[
    Choice(
      title: 'Home',
      icon: Icons.home,
      customValue: false,
    ),
    Choice(title: 'Contact', icon: Icons.contacts, customValue: false),
    Choice(title: 'Map', icon: Icons.map, customValue: false),
    Choice(title: 'Phone', icon: Icons.phone, customValue: false),
    Choice(title: 'Camera', icon: Icons.camera_alt, customValue: false),
  ];
  List<Choice> selectedList = [];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text("Check List View"),
        ),
        body: SingleChildScrollView(
          child: Column(
            children: [optionsList(),
              displayList()],
          ),
        ));
  }

  optionsList() {
    return Container(
      color: Colors.red,
      child: ListView.builder(
        shrinkWrap: true,
        itemCount: choices.length,
        itemBuilder: (BuildContext context, int index) {
          return Column(
            mainAxisSize: MainAxisSize.max,
            children: [
              Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Text(
                    choices[index].title,
                    style: TextStyle(fontSize: 30),
                  ),
                  Checkbox(
                      value: choices[index].customValue,
                      onChanged: (value) async {
                        setState(
                          () {
                            choices[index].customValue = value!;
                           if( selectedList.contains( choices[index])){
                             selectedList.remove(choices[index]);
                           }else{
                             selectedList.add(choices[index]);
                           }

                            // choices[index].customValue = value!;
                            // if (choices[index].customValue == true) {
                            //   selectedList.add(choices[index]);
                            // } else if (choices[index].customValue == false) {
                            //   selectedList.remove(choices[index].title);
                            // }
                          },
                        );
                        // debugPrint(jsonEncode(selectedList.toString()));
                      }
                      ),
                ],
              ),
            ],
          );
        },
      ),
    );
  }
  displayList() {
    return Container(
      height: MediaQuery.of(context).size.height / 1.5,
      width: MediaQuery.of(context).size.width,
      color: Colors.yellow,
      child: ListView.builder(
          itemCount: selectedList.length,
          itemBuilder: (BuildContext context, int index) {
            return Container(
                alignment: Alignment.center,
                child: Text(
                  selectedList[index].title,
                  style: TextStyle(fontSize: 30),
                ));
            // Text("Selected Items ${selectedList.}")
          }),
    );
  }
}

class Choice {
  Choice({required this.title, required this.icon, required this.customValue});

  String title;
  IconData icon;
  bool customValue;
}


Code custom checkbox
import 'package:listview_checkbox_secondtry/exports.dart';
class CustomCheck extends StatefulWidget {
  late bool? customvalue;

  CustomCheck({Key? key,this.customvalue,
    // required this.setState
  }) : super(key: key);

  @override
  State<CustomCheck> createState() => _CustomCheckState();
}

class _CustomCheckState extends State<CustomCheck> {
  late bool? customvalue;
  @override
  Widget build(BuildContext context) {
    return Checkbox(
        value: customvalue,
        onChanged: (bool? value) {
          customvalue = value;
          setState(() {});
        });
  }
}
