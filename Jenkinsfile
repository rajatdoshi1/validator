#!/usr/bin/env groovy

import groovy.transform.Field;

//Vaidation dependency
import java.io.File;
import java.io.IOException;

import javax.xml.XMLConstants;
import javax.xml.transform.stream.StreamSource;
import javax.xml.validation.Schema;
import javax.xml.validation.SchemaFactory;
import javax.xml.validation.Validator;

import org.xml.sax.SAXException;


def jenkinsNodeType = 'linux'

node() {
    echo 'Processing started'

    stage('Checkout') {
        checkout scm
    }
    stage("validate schema"){
            utils.validateXMLSchema("schema.xsd", "Create_New_AD_Account.xml" )
    }
    echo 'Processing Ended'
}

def validateXMLSchema(String xsdPath, String xmlPath){
        SchemaFactory factory = 
                SchemaFactory.newInstance("http://www.w3.org/2001/XMLSchema");
        Schema schema = factory.newSchema(new File(xsdPath));
        Validator validator = schema.newValidator();
        validator.validate(new StreamSource(new File(xmlPath)));
        return true;
}