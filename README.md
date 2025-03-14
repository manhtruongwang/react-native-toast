# react-native-alert-dialog

## Example Dialog Box

|                                                                           Theme Light                                                                           |                                                                          Theme Dark                                                                           |
| :-------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------: |
| <img src="https://github.com/manhtruongwang/react-native-toast-dialog/blob/master/.github/images/dialog-light.gif?raw=true" height="350" alt="Dialogs light" /> | <img src="https://github.com/manhtruongwang/react-native-toast-dialog/blob/master/.github/images/dialog-dark.gif?raw=true" height="350" alt="Dialogs Dark" /> |

## Example Toast Notification

|                                                                          Theme Light                                                                          |                                                                         Theme Dark                                                                          |
| :-----------------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------: |
| <img src="https://github.com/manhtruongwang/react-native-toast-dialog/blob/master/.github/images/toast-light.gif?raw=true" height="350" alt="toasts light" /> | <img src="https://github.com/manhtruongwang/react-native-toast-dialog/blob/master/.github/images/toast-dark.gif?raw=true" height="350" alt="toasts Dark" /> |

## Installation

### - Installing:

```sh
yarn add react-native-alert-dialog
```

### - Installing dependencies:

- For Native project:

```sh
yarn add react-native-safe-area-context

pod install
```

- For Expo project:

```sh
expo install react-native-safe-area-context
```

## Usage

```tsx
import { ALERT_TYPE, Dialog, AlertNotificationRoot, Toast } from 'react-native-alert-notification';

<AlertNotificationRoot>
  <View>
    // dialog box with single button
    <Button
      title={'dialog box'}
      onPress={() =>
        Dialog.show({
          type: ALERT_TYPE.SUCCESS,
          title: 'Success',
          textBody: 'Congrats! this is dialog box success',
          button: 'close',
        })
      }
    />
    // dialog box with cancel & confirm buttons
    <Button
      title={'confirmation dialog'}
      onPress={() =>
        Dialog.show({
          type: ALERT_TYPE.WARNING,
          title: 'Confirm Action',
          textBody: 'Are you sure you want to proceed with this action?',
          cancelButton: 'Cancel',
          confirmButton: 'Proceed',
          onPressCancel: () => console.log('Action cancelled'),
          onPressConfirm: () => console.log('Action confirmed'),
        })
      }
    />
    // toast notification
    <Button
      title={'toast notification'}
      onPress={() =>
        Toast.show({
          type: ALERT_TYPE.SUCCESS,
          title: 'Success',
          textBody: 'Congrats! this is toast notification success',
          paddingTop: 45, // custom top padding
        })
      }
    />
  </View>
</AlertNotificationRoot>;
```

## Documentation:

### Root Component

A React node that will be most likely wrapping your whole app.

| Name         | Description                                  | Require | Default | Type                                                                                                |
| ------------ | -------------------------------------------- | ------- | ------- | --------------------------------------------------------------------------------------------------- |
| theme        | select theme light dark (by default is auto) |         | auto    | 'light','dark'                                                                                      |
| colors       | custom colors                                |         |         | [IColors<light>, IColors<dark>]                                                                     |
| dialogConfig | config dialog box global                     |         |         | {closeOnOverlayTap:bool, autoClose:bool / number}                                                   |
| toastConfig  | config toast global                          |         |         | {autoClose:bool / number, titleStyle?: StyleProp<TextStyle> , textBodyStyle?: StyleProp<TextStyle>} |

```ts
type IProps = {
  dialogConfig?: Pick<IConfigDialog, 'closeOnOverlayTap' | 'autoClose'>;
  toastConfig?: Pick<IConfigToast, 'autoClose' | 'titleStyle' | 'textBodyStyle'>;
  theme?: 'light' | 'dark';
  colors?: [IColors, IColors] /** ['light_colors' , 'dark_colors'] */;
};
type IColors = {
  label: string;
  card: string;
  overlay: string;
  success: string;
  danger: string;
  warning: string;
};
```

### Dialog Box Component

| Name              | Description                                        | Require | Default | Type                           |
| ----------------- | -------------------------------------------------- | ------- | ------- | ------------------------------ |
| title             | The title text                                     |         |         | String                         |
| type              | Defines the type ("Success", "Warning" or "Error") | true    |         | "SUCCESS", "DANGER", "WARNING" |
| textBody          | The text body                                      |         |         | String                         |
| button            | name button (for hide button: undefined)           |         |         | String                         |
| cancelButton      | Text for cancel button in dual-button layout       |         |         | String                         |
| confirmButton     | Text for confirm button in dual-button layout      |         |         | String                         |
| autoClose         | Defines time auto close dialog box in ms           |         | face    | bool / number                  |
| closeOnOverlayTap | allow close if click in overlay                    |         | true    | bool                           |
| onPressButton     | (if not declared and isset button action is close) |         | String  | () => void                     |
| onPressCancel     | Action when cancel button is pressed               |         |         | () => void                     |
| onPressConfirm    | Action when confirm button is pressed              |         |         | () => void                     |
| onShow            | action after end animation open                    |         |         | () => void                     |
| onHide            | action after end animation close                   |         |         | () => void                     |

```ts
type IConfig = {
  type: ALERT_TYPE;
  title?: string;
  textBody?: string;
  button?: string;
  cancelButton?: string;
  confirmButton?: string;
  autoClose?: number | boolean;
  closeOnOverlayTap?: boolean;
  onPressButton?: () => void;
  onPressCancel?: () => void;
  onPressConfirm?: () => void;
  onShow?: () => void;
  onHide?: () => void;
};
```

### Toast Notification Component

| Name       | Description                                        | Require | Default | Type                           |
| ---------- | -------------------------------------------------- | ------- | ------- | ------------------------------ |
| title      | The title text                                     |         |         | String                         |
| type       | Defines the type ("Success", "Warning" or "Error") |         |         | "SUCCESS", "DANGER", "WARNING" |
| textBody   | The text body                                      |         |         | String                         |
| autoClose  | Defines time auto close dialog box in ms           |         | 5000    | bool / number                  |
| paddingTop | Specify custom top padding                         |         | 0       | number                         |
| onPress    | action click in card                               |         |         | bool                           |
| onShow     | event after end animation open                     |         |         | () => void                     |
| onHide     | event after end animation close                    |         |         | () => void                     |

```ts
type IConfig = {
  type?: ALERT_TYPE;
  title?: string;
  textBody?: string;
  autoClose?: number | boolean;
  paddingTop?: number;
  titleStyle?: StyleProp<TextStyle>;
  textBodyStyle?: StyleProp<TextStyle>;
  onPress?: () => void;
  onShow?: () => void;
  onHide?: () => void;
};
```

### For Close popup

```ts
// For Dialog Box
Dialog.hide();

// For Toast Notification
Toast.hide();
```

## Author

Truong Quang Manh | [https://vietgigs.vn](https://vietgigs.vn)

See the contributing guide to learn how to contribute to the repository and the development workflow.

## License

MIT
