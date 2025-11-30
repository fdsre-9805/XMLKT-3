<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

    <xsl:key name="teacher-key" match="course" use="teachers/teacher"/>
    <xsl:key name="keyword-key" match="course" use="keywords/keyword"/>

    <xsl:template match="/">
        <html>
            <head>
                <title>Наши курсы</title>
            </head>
            <body>
                <h1>Наши курсы</h1>

                <h3>Курсы, которые ведет Борисов И.О.</h3>
                <ul>
                    <xsl:for-each select="key('teacher-key', 'Борисов И.О.')">
                        <xsl:sort select="title"/>
                        <li><xsl:value-of select="title"/></li>
                    </xsl:for-each>
                </ul>

                <h3>Курсы, которые используют XML</h3>
                <ul>
                    <xsl:for-each select="key('keyword-key', 'XML')">
                        <xsl:sort select="title"/>
                        <li><xsl:value-of select="title"/></li>
                    </xsl:for-each>
                </ul>

                <h3>Курсы Борисова И.О. с темой XSLT</h3>
                <ul>
                    <xsl:for-each select="key('teacher-key', 'Борисов И.О.')">
                        <xsl:if test="keywords/keyword = 'XSLT'">
                            <li><xsl:value-of select="title"/></li>
                        </xsl:if>
                    </xsl:for-each>
                </ul>

            </body>
        </html>
    </xsl:template>

</xsl:stylesheet>
