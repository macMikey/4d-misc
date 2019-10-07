// converts icons from 4d projects in the v6, 2004, etc. eras to v2013 and beyond, where PICT is not a valid icon type any longer
// Method: Convert_Picture_Library_Tom
  // ----------------------------------------------------
  // User name (OS): Tom Benedict
  // Date and time: 7/10/2019, 14:03:11
  // ----------------------------------------------------
  // Description
  // Note: This method will find and update any images in the Picture Library  in PICT format
  //           which are not compatible with 64bit.
  // Note: !!! This method must be run in 32bit. !!!
  //
C_LONGINT($i;$SOA;$RIS;$PictRef)
C_TEXT($PictName)
C_PICTURE($Pict)

If (Version type ?? 64 bit version)  // running in 64bit
          // do nothing. Must be run in 32bit
Else
          //------------ initialize arrays ------------------
        ARRAY LONGINT($aL_PictRef;0)
        ARRAY TEXT($aT_PictName;0)
        ARRAY TEXT($at_Codecs;0)
        PICTURE LIBRARY LIST($aL_PictRef;$aT_PictName)
        $SOA:=Size of array($aL_PictRef)

          //------------ convert PICT to png ------------------
        If ($SOA>0)
                For ($i;1;$SOA)  // for each image
                        $PictRef:=$aL_PictRef{$i}
                        $PictName:=$aT_PictName{$i}
                        GET PICTURE FROM LIBRARY($aL_PictRef{$i};$Pict)
                        GET PICTURE FORMATS($Pict;$at_Codecs)
                        For ($j;1;Size of array($at_Codecs))
                                If ($at_Codecs{$j}=".pict")  // if the format is obsolete
                                        CONVERT PICTURE($Pict;".png")  // conversion to png
                                        TRANSFORM PICTURE($Pict;Transparency;0x00FFFFFF)  // make the background transparent
                                          // and store in library
                                        SET PICTURE TO LIBRARY($Pict;$PictRef;$PictName)
                                End if
                        End for
                End for
        Else
                ALERT("The image libary is empty.")
        End if
End if
  //------------ end of method ------------------
