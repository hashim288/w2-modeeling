# w2-modeeling
package w2;

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

/**
 *
 * @author  Gary Allen
 * @version 3
 * Thanks to Ron and Anne
 */

public class SwDiaExamp extends JDialog {

    private Container cp;

    private Box boxSelection;
    private Box boxSelectionRes;
    private Box boxButtons;

    private JLabel jlblSel;
    private JComboBox jcmbSel;
    private JCheckBox jchkShowRes;
    private JTextField jtxtRes;
    private JButton jcmdOK;
    private JButton jcmdCancel;
    private JPanel jpanButtons;

    /**
     * SwDiaExamp constructor method
     */
    public SwDiaExamp(SwExamp parent, boolean modal) {

        super (parent, modal); // call JDialog constructor

        boxSelection = Box.createHorizontalBox();
        boxSelectionRes = Box.createHorizontalBox();
        boxButtons = Box.createHorizontalBox();

        jlblSel = new JLabel("Select Item");

        jcmbSel = new JComboBox();
        jcmbSel.addItem("Apples");
        jcmbSel.addItem("Pears");
        jcmbSel.addItem("Plums");
        jcmbSel.addItem("Grapes");
        jcmbSel.addItem("Pinapple");
        jcmbSel.addItem("g");




        // add combo box action listener - anonymous object
        jcmbSel.addActionListener (new ActionListener () {
            public void actionPerformed (ActionEvent evt) {
                doSelectionUpdate(); // calls another method to do the work
            }
        }    );


        // vertical Box layout
        cp = getContentPane();
        cp.setLayout (new BoxLayout (cp, 1));


        // put GUI components in the correct box
        boxSelection.add(Box.createHorizontalStrut(10));
        boxSelection.add (jlblSel);
        boxSelection.add(Box.createHorizontalStrut(10));
        boxSelection.add (jcmbSel);
        boxSelection.add(Box.createHorizontalGlue());

        cp.add(boxSelection);


        //now the next box
        jchkShowRes = new JCheckBox("Show Selections");
        jchkShowRes.setSelected(true);

        jtxtRes = new JTextField("No Selection Made");

        boxSelectionRes.add(jchkShowRes);
        boxSelectionRes.add(jtxtRes);


        // force some space below selection box
        cp.add(Box.createVerticalStrut(10));
        cp.add(boxSelectionRes);


        // Now the button box but first put them into a panel
        // with a nice border
        jpanButtons = new JPanel();

        jpanButtons.setBorder (new javax.swing.border.BevelBorder(0));
        jpanButtons.setLayout(new javax.swing.BoxLayout (jpanButtons, 0));


        // add buttons and listeners
        jcmdOK = new JButton("OK");
        jcmdOK.addActionListener (new ActionListener () {
            public void actionPerformed (ActionEvent evt) {
                setVisible (false);
                dispose ();
            }
        }    );

        jcmdCancel = new JButton("Cancel");
        jcmdCancel.addActionListener (new ActionListener () {
            public void actionPerformed (ActionEvent evt) {
                setVisible (false);
                dispose ();
            }
        }    );

        jpanButtons.add(jcmdOK);
        jpanButtons.add(jcmdCancel);

        getContentPane().add(Box.createVerticalStrut(10));
        getContentPane().add(jpanButtons);
        pack();
    }


    /**
     * this is the action we perform when a combo box selection is made.
     */
    private void doSelectionUpdate(){
        if(jchkShowRes.isSelected()) {
            jtxtRes.setText("Selected fruit is "+jcmbSel.getSelectedItem());
        }
    }
}
