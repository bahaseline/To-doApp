
# To-do React Native Expo App

This is a simple Task Manager application built with React Native using Expo. The app allows users to add, view, and delete tasks, helping them manage their daily activities.

## Features

- Add new tasks.
- View a list of tasks.
- Mark tasks as complete.


## Installation

Clone the repository:

```bash
git clone https://github.com/bahaseline/To-doApp.git
cd task-manager-app
```

Install dependencies:
```bash
npm install
# or
yarn install
```

Start the Expo server:
```bash
npx expo start
```

Running on a Device or Emulator:
- Expo Go App: Scan the QR code generated by the Expo server with the Expo Go app on your iOS or Android device.
- Emulator: Use Android Studio or Xcode to run the app on an emulator.

## Screenshot

<div style="text-align: center;">
  <img src="https://github.com/bahaseline/To-doApp/assets/117291953/f9d3b42f-d88f-4234-abb1-f5b1f404ee78" alt="Screenshot" style="width: 50%; max-width: 100%;">
</div>


## Usage/Examples


Adding a Task
- Enter the task description in the "Write a task" input field.
- Press the "+" button to add the task to the list.

Completing a Task

- Tap on a task to mark it as complete and remove it from the list.

Components
Task Component

- The Task component displays an individual task item with styles.

Props:

text (string): The task text to display.

Code:

```javascript
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

const Task = (props) => {
    return (
        <View style={styles.item}>
            <View style={styles.itemLeft}>
                <View style={styles.square}></View>
                <Text style={styles.itemText}>{props.text}</Text>
            </View>
            <View style={styles.circular}></View>
        </View>
    );
};

const styles = StyleSheet.create({
    item: {
        backgroundColor: '#FFF',
        padding: 15,
        borderRadius: 10,
        flexDirection: 'row',
        alignItems: 'center',
        justifyContent: 'space-between',
        marginBottom: 20,
    },
    itemLeft: {
        flexDirection: 'row',
        alignItems: 'center',
        flexWrap: 'wrap'
    },
    square: {
        width: 24,
        height: 24,
        backgroundColor: '#ff6699',
        opacity: 0.4,
        borderRadius: 5,
        marginRight: 15,
    },
    itemText: {
        maxWidth: '80%',
    },
    circular: {
        width: 12,
        height: 12,
        borderColor: '#ff6699',
        borderWidth: 2,
        borderRadius: 5,
    },
});

export default Task;
```

Main App Component
The App component manages the state of tasks and renders the task input and list.

Code:

```javascript
import React, { useState } from 'react';
import {
    Keyboard,
    KeyboardAvoidingView,
    Platform,
    StyleSheet,
    Text,
    TextInput,
    TouchableOpacity,
    View
} from 'react-native';
import Task from "./components/Task";

export default function App() {
    const [task, setTask] = useState();
    const [taskItems, setTaskItems] = useState([]);

    const handleAddTask = () => {
        Keyboard.dismiss();
        setTaskItems([...taskItems, task]);
        setTask(null);
    };

    const completeTask = (index) => {
        let itemsCopy = [...taskItems];
        itemsCopy.splice(index, 1);
        setTaskItems(itemsCopy);
    };

    return (
        <View style={styles.container}>
            <View style={styles.taskWrapper}>
                <Text style={styles.sectionTitle}>Today's Tasks</Text>
                <View style={styles.items}>
                    {taskItems.map((item, index) => (
                        <TouchableOpacity key={index} onPress={() => completeTask(index)}>
                            <Task key={index} text={item} />
                        </TouchableOpacity>
                    ))}
                </View>
            </View>
            <KeyboardAvoidingView
                behavior={Platform.OS === "ios" ? "padding" : "height"}
                style={styles.writeTaskWrapper}
            >
                <TextInput
                    style={styles.input}
                    placeholder={'Write a task'}
                    value={task}
                    onChangeText={text => setTask(text)}
                />
                <TouchableOpacity onPress={() => handleAddTask()}>
                    <View style={styles.addWrapper}>
                        <Text style={styles.addText}>+</Text>
                    </View>
                </TouchableOpacity>
            </KeyboardAvoidingView>
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        backgroundColor: '#E8EAED',
    },
    taskWrapper: {
        paddingTop: 80,
        paddingHorizontal: 20,
    },
    sectionTitle: {
        fontSize: 24,
        fontWeight: 'bold',
    },
    items: {
        marginTop: 30,
    },
    writeTaskWrapper: {
        position: 'absolute',
        bottom: 60,
        width: '100%',
        flexDirection: 'row',
        justifyContent: 'space-around',
        alignItems: 'center',
    },
    input: {
        paddingVertical: 20,
        paddingHorizontal: 15,
        width: 250,
        backgroundColor: '#FFF',
        borderRadius: 60,
        borderColor: '#C0C0C0',
        borderWidth: 1,
        marginLeft: 20,
    },
    addWrapper: {
        width: 60,
        height: 60,
        backgroundColor: '#FFF',
        borderRadius: 60,
        justifyContent: 'center',
        alignItems: 'center',
        borderColor: '#C0C0C0',
        borderWidth: 1,
        marginRight: 30,
    },
    addText: {},
});

```
## Contributing

Contributions are welcome! Please fork this repository and submit a pull request for any feature enhancements, bug fixes, or improvements.


## License

This project is licensed under the MIT License. See the LICENSE file for details.
