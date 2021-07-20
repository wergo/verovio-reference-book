The method performs a lookup in the loaded MEI tree and will return all attributes for the retrieved element. This includes attributes currently not supported by Verovio. Looking in the MEI tree means that looking for elements added dynamically for the rendering by Verovio will no be found. This is the case for `system` elements when loading score-based MEI, or `meterSig` or `clef` elements displayed at the beginning of a system.
