import xml.etree.ElementTree as ET
import os
from os import walk


def getfiles(directoryname):
    files = []
    for (dirpath, dirnames, filenames) in walk(directoryname):
        for (currentfile) in filenames:
            files.append(dirpath + os.sep + currentfile)
        break
    return files


def getworkingfolder():
    for (dirpath, dirnames, filenames) in walk(os.path.dirname(os.path.abspath(__file__))):
        for (dirname) in dirnames:
            return dirname


def toxml(filename):
    return ET.parse(filename)


def addtoset(elements, xml):
    for (element) in xml.getroot().findall('Purchase'):
        if ET.tostring(element) in elements:
            print 'Duplicate found'
        else:
            elements.add(ET.tostring(element))


def printset(elements, filename, mode):
    f = open(filename, mode)
    f.write('<?xml version="1.0"?>\n<Purchases>')
    for (element) in elements:
        f.write(element)
    f.write('</Purchases>')
    f.close()


def gettestfiles():
    files = []
    for (dirpath, dirnames, filenames) in walk(os.path.dirname(os.path.abspath(__file__))):
        for (filename) in filenames:
            if filename.endswith('.xml'):
                print(filename)
                files.append(filename)
        break
    return files


def buildcanon(directory):
    elements = set()
    for (filename) in getfiles(directory):
        addtoset(elements, toxml(filename))
    printset(elements, getcanonpath(directory), 'w')


def createuploadfile(directory, filename):
    xml = ET.parse(filename)
    canon = set()
    output = set()
    addtoset(canon, ET.parse(getcanonpath(directory)))
    for (element) in xml.getroot():
        if not(ET.tostring(element) in canon):
            output.add(ET.tostring(element))
    addtoset(canon, xml)
    printset(output, 'upload-' + filename + '.xml', 'w')
    printset(canon, getcanonpath(directory), 'w')


def getcanonpath(directory):
    return directory + os.sep + directory + '-canon.xml'


def main():
    print "Working"
    for (filename) in gettestfiles():
        if filename.startswith('upload-'):
            break
        directory = filename.split('-')[-1].split('.')[0]
        if not (os.path.isdir(directory)):
            os.mkdir(directory)
        if not(os.path.isfile(getcanonpath(directory))):
            buildcanon(directory)
        createuploadfile(directory, filename)
        os.rename(filename, directory + os.sep + filename)

if __name__ == "__main__":
    main()
