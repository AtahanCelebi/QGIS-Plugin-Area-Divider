.. AreaDivider documentation master file, created by
   sphinx-quickstart on Tue Jan 19 18:58:29 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

QGIS Plugin Area Divider 
=======================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:
	
.. admonition:: Unit Test

This **unit test** work for the layer if it has been added or not and check its suitability

**Test Layer Transaction**
-Qgis Project instance/Add map layer whether layer exist
-try/except raise error if not exist could not pass unit test

**Test Load Layer**
-Read the layer
-If None could not pass unit test

**Here is the all code that we implement**::

    class SaveAttributesTest(unittest.TestCase):
    	"""Test dialog works."""
    	@classmethod
    	def setUpClass(cls):
        	cls.iface = get_iface()
    	def setUp(self):
        	"""Runs before each test."""
        	QgsProject.instance().clear()
        	self.dialog = SaveAttributesDialog(None)
        	self.attributes=SaveAttributes(get_iface())
        	self.attributes.dlg=self.dialog
    	def test_Layer(self):
        	try:
            		vlayer = QgsVectorLayer("TEST_LINE","line","memory")
            		vlayer = QgsVectorLayer("TEST_LINE","point","memory")
            		vlayer = QgsVectorLayer("TEST_LINE","polygon","memory")

        	except:
            		self.assertTrue(True==False)

    	def test_Layer_Transaction(self):
        	try:
            		vlayer = QgsVectorLayer("TEST_LINE","line","memory")
            		QgsProject.instance().addMapLayer(vlayer)

        	except:
            		self.assertTrue(True==False)       

    	def test_load_layer(self): 
        	path=os.path.dirname(os.path.realpath(__file__)) + "../../save_attributes/unittests/"                                               
        	ds = ogr.Open(path+"c_beytepe.shp",0)
        	self.assertTrue(ds==None)

    	def tearDown(self):
        	"""Runs after each test."""
        	self.dialog = None


	if __name__ == "__main__":
    	suite = unittest.makeSuite(SaveAttributesDialogTest)

    	logging.basicConfig(stream=sys.stderr, level=logging.DEBUG)
    	runner = unittest.TextTestRunner(verbosity=2)
    	runner.run(suite)
