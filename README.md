# JIMP Implementation (React)
An example async implementation of Jimp image processing library. It was used with React in this project, but it's ready for any framework you throw at it!

More information about JIMP is here:
* JIMP: https://github.com/oliver-moran/jimp 

## The function
You can call the function like this: `ProcessImage(image,crop,context)`

The function takes 3 parameters, the last two are optional.
- 1st param refers to the image like this `let file = event.target.files[0];`
- 2nd param refers to the crop settings which you are free to change. For example, `"squarePicture"` or `"landscapePicture"`
- 3rd param refers to the "this" scope of the file you call the function from. This is useful if you want to call a function defined in a given scope. I called the `context.setUploadProgress` to update React's state in the context scope and display an image processing progress bar for the user.

The function returns a Base64 image.

## Example code

Import the function in another JS file: 
`import ProcessImage from "../../services/imageProcessing";`

Immediately execute the function when a new file is added (only 1 file at a time here):
```javascript
  onChangeFile = (event) => {
    //setting the file to the input
    if (event.target.files[0]) {
      let image = event.target.files[0];
      let context = this;
      //calling the image processing function
      (async function () {
        context.setState({ hiddenProgress: false });
        let image = await ProcessImage(image, "squarePicture", context);
        if (image && context !== undefined) {
          context.setState({ picture: image });
        }
      })();
    }
  };
```
  Function to update React's state (assumes uploadProgress is defined):
```javascript
    setUploadProgress = (progress) => {
    this.setState({ uploadProgress: progress });
  };
```
