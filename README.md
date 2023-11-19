# javafx-informations
A collection of useful informations about JavaFX.

## Method execution order in controllers when loading a FXML file

If you are on a Scene you can load a new FXML file like this:

    public static void switchSceneContent(String fxmlFileUrl) throws IOException {
        FXMLLoader loader = new FXMLLoader(MainApplication.class.getResource(fxmlFileUrl));
        mainStage.getScene().setRoot(loader.load());
        NewViewController viewController = loader.getController();
        viewController.init();
    }

The controller of the new view could look like this:

    public class NewViewController implements Initializable {
    
        public NewViewController() {
            System.out.println("#1. Constructor()");
            Platform.runLater(() -> System.out.println("#4. Platform.runLater()"));
        }
    
        public void init() {
            System.out.println("#3. init()");
        }
    
        @Override
        public void initialize(URL location, ResourceBundle resources) {
            System.out.println("#2. initialize()");
        }
    
    }

The order of these methods is:

    Console:
    1. Constructor()
    2. initialize()
    3. init()
    4. Platform.runLater()
