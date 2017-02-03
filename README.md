C# XML-Parser

public string GetValue(string XMLInput, string XMLtagValue)
        {
            string retval = string.Empty, FirstXMLtagValue = string.Empty, LastXMLtagValue = string.Empty;
            FirstXMLtagValue = "<" + XMLtagValue + ">";
            LastXMLtagValue = "</" + XMLtagValue + ">";
            if (XMLInput.IndexOf(XMLtagValue) != -1)
            {
                string newRetVal = string.Empty;
                retval = XMLInput.Substring(XMLInput.IndexOf(FirstXMLtagValue));
                retval = retval.Substring(FirstXMLtagValue.Length);
                retval = retval.Substring(0, retval.IndexOf(LastXMLtagValue));
            }
            return retval;
        }

        public DataSet sdam(string xmlData)
        {
            string AcName = string.Empty;
            DataSet ds = new DataSet("NewDataSet");
            ds.ReadXml(new XmlTextReader(new StringReader(xmlData)));
            foreach (DataTable table in ds.Tables)
            {
                foreach (DataRow dr in table.Rows)
                {
                    if (dr["FieldID"].ToString() == "127")
                        AcName = dr["FieldValue"].ToString();
                }
            }

            return ds;
        }

        public DataTable stam(string xmlData)
        {
            StringReader theReader = new StringReader(xmlData);
            DataSet theDataSet = new DataSet();
            try
            {
                theDataSet.ReadXml(theReader);
            }
            catch (Exception ex)
            { }

            return theDataSet.Tables[0];
        }
