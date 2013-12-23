% --- GERAINT HARRIES - 1100682

function varargout = guidepush(varargin)

gui_Singleton = 1;
gui_State = struct('gui_Name',       mfilename, ...
                   'gui_Singleton',  gui_Singleton, ...
                   'gui_OpeningFcn', @guidepush_OpeningFcn, ...
                   'gui_OutputFcn',  @guidepush_OutputFcn, ...
                   'gui_LayoutFcn',  [] , ...
                   'gui_Callback',   []);
if nargin && ischar(varargin{1})
    gui_State.gui_Callback = str2func(varargin{1});
end
if nargout
    [varargout{1:nargout}] = gui_mainfcn(gui_State, varargin{:});
else
    gui_mainfcn(gui_State, varargin{:});
end


function guidepush_OpeningFcn(hObject, handles, varargin)

handles.output = hObject;

guidata(hObject, handles);

function varargout = guidepush_OutputFcn(hObject, eventdata, handles) 
varargout{1} = handles.output;

% --- Executes on slider movement.
function Contrast_Callback(hObject, eventdata, handles)
% hObject    handle to Contrast (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider


% --- Executes during object creation, after setting all properties.
function Contrast_CreateFcn(hObject, eventdata, handles)
% hObject    handle to Contrast (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: slider controls usually have a light gray background.
if isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor',[.9 .9 .9]);
end


% --- Executes on slider movement.
function Brightness_Callback(hObject, eventdata, handles)
% hObject    handle to Brightness (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global Picture;
value = 0;
value = get(hObject,'Value')*100;
Picture = Picture + value;
imshow(Picture)
% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider


% --- Executes during object creation, after setting all properties.
function Brightness_CreateFcn(hObject, eventdata, handles)
% hObject    handle to Brightness (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: slider controls usually have a light gray background.
if isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor',[.9 .9 .9]);
end

% --- Executes on button press in BW.
function BW_Callback(hObject, eventdata, handles)
% hObject    handle to BW (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global Picture;
global isGray; 
Picture = im2bw(Picture);
isGray = 1;
imshow(Picture)

function untitled_OpeningFcn(hObject, eventdata, handles, varargin)
handles.output = hObject;
handles.cdir = pwd;
set(handles.listbox1,'enable','off');
guidata(hObject, handles);

% --- Executes on button press in Open.
function Open_Callback(hObject, eventdata, handles)
% hObject    handle to Open (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global Picture;
global filename;
global pathname;
[filename, pathname] = uigetfile({'*.jpg';'*.png';'*.jpeg';'*.ai';'*.bmp';'*.emf';'*.fig';'*.pbm';'*.pcx';'*.pdf';'*.pgm';'*.png';'*.ppm';'*.tif'}, 'Pick a photo');
A = strcat(pathname, filename);
Picture = imread(A);
cheese = imshow(Picture);


% --- Executes on button press in Save.
function Save_Callback(hObject, eventdata, handles)
% hObject    handle to Save (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global filename;
global pathname;

[filename, pathname] = uiputfile({'*.jpg';'*.png';'*.jpeg';'*.ai';'*.bmp';'*.emf';'*.fig';'*.pbm';'*.pcx';'*.pdf';'*.pgm';'*.png';'*.ppm';'*.tif'},'Save as');

saveas(gcf, filename, 'jpg')
%{'jpg;bmp;emf;eps;fig;jpg;pbm;pcx;pdf;pgm;png;ppm;tif'})


% --- Executes on button press in Grey.
function Grey_Callback(hObject, eventdata, handles)
% hObject    handle to Grey (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global Picture;
global isGray; 
Picture = rgb2gray(Picture);
isGray = 1;
imshow(Picture)


% --- Executes on button press in Rotate.
function Rotate_Callback(hObject, eventdata, handles)
% hObject    handle to Rotate (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global Picture;
Picture = imrotate(Picture, 90);
imshow(Picture)


% --- Executes on button press in VerticleFlip.
function VerticleFlip_Callback(hObject, eventdata, handles)
% hObject    handle to VerticleFlip (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global Picture;
Picture = flipdim(Picture, 1);
imshow(Picture)


% --- Executes on button press in HorizontalFlip.
function HorizontalFlip_Callback(hObject, eventdata, handles)
% hObject    handle to HorizontalFlip (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global Picture;
Picture = flipdim(Picture, 2);
imshow(Picture)

% --- Executes on button press in Crop.
function Crop_Callback(hObject, eventdata, handles)
% hObject    handle to Crop (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global Picture;
Picture = imcrop(Picture);
imshow(Picture)

% --- Executes on slider movement.
function slider6_Callback(hObject, eventdata, handles)
% hObject    handle to slider6 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider
global Picture;
value = 0;
value = get(hObject,'Value')*100;
Picture = imrotate(Picture, value);
imshow(Picture + value)

% --- Executes during object creation, after setting all properties.
function slider6_CreateFcn(hObject, eventdata, handles)
% hObject    handle to slider6 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: slider controls usually have a light gray background.
if isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor',[.9 .9 .9]);
end

% --- Executes on button press in FishEye.
function FishEye_Callback(hObject, eventdata, handles)
% hObject    handle to FishEye (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global Picture;
Picture = lensdistort(Picture, 2);
imshow(Picture)


% --- Executes on selection change in listbox1.
function listbox1_Callback(hObject, eventdata, handles)
% hObject    handle to listbox1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: contents = cellstr(get(hObject,'String')) returns listbox1 contents as cell array
%        contents{get(hObject,'Value')} returns selected item from listbox1

% --- Executes during object creation, after setting all properties.
function listbox1_CreateFcn(hObject, eventdata, handles)
% hObject    handle to listbox1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: listbox controls usually have a white background on Windows.
%       See ISPC and COMPUTER.
if ispc && isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor','white');
end


% --- Executes on button press in Instagram.
function Instagram_Callback(hObject, eventdata, handles)
% hObject    handle to Instagram (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global Picture;
global isGray; 
if isGray ~= 0
    Picture = rgb2gray(Picture);
end
Picture = retro_filter_vectorized(Picture,0.1, 0.5, 0.3, 0.5, 0.05);
imshow(Picture)

% --- Executes on button press in Edge.
function Edge_Callback(hObject, eventdata, handles)
% hObject    handle to Edge (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global Picture;
global isGray; 
if isGray ~= 0
    Picture = rgb2gray(Picture);
end
Picture = edge(Picture, 'sobel');
imshow(Picture);

% --- Executes on button press in Blur.
function Blur_Callback(hObject, eventdata, handles)
% hObject    handle to Blur (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global Picture;
h = fspecial('gaussian', 4, 4);
Picture = imfilter(Picture, h);
imshow(Picture);
