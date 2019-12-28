# matlab
Matlab scripts and other matlab things to remember and use

## Cursor Script to add precision

The main things of this part were taken from the reply of **gnovice** in:
https://stackoverflow.com/questions/5961034/how-can-i-display-numbers-with-higher-precision-in-a-matlab-data-cursor

So, to add precision in the cursors, just right-click on the cursor window and then select *Edit update function...*

```matlab
function output_txt = myfunction(obj,event_obj)
% Display the position of the data cursor
% obj          Currently not used (empty)
% event_obj    Handle to event object
% output_txt   Data cursor text string (string or cell array of strings).

pos = get(event_obj,'Position');
output_txt = {['X: ',num2str(pos(1),7)],...
    ['Y: ',num2str(pos(2),7)]};

% If there is a Z-coordinate in the position, display it as well
if length(pos) > 2
    output_txt{end+1} = ['Z: ',num2str(pos(3),7)];
end
```

In the previous example I already took the num2str(pos(i),NN) to NN=7, meaning that the precision will be 7 digits. 

Now your datatip text should display more precision for your numbers. If you want to accomplish all of the above programmatically, you would first create your text update function, save it to a file (like 'updateFcn.m'), then turn on Data Cursors using the function datacursormode and set them to use your user-defined text update function. Here's an example:


plot(1:10, rand(1, 10));  % Plot some sample data
dcmObj = datacursormode;  % Turn on data cursors and return the
                          %   data cursor mode object
set(dcmObj, 'UpdateFcn', @updateFcn);  % Set the data cursor mode object update
                                       %   function so it uses updateFcn.m
