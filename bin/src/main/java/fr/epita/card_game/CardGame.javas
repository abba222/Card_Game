/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package fr.epita.card_game;

import com.jakewharton.fliptables.FlipTableConverters;
import java.util.Arrays;
import java.util.Random;
import java.util.LinkedList;
import javax.xml.parsers.*;
import javax.xml.transform.*;
import javax.xml.transform.dom.*;
import javax.xml.transform.stream.*;
import org.w3c.dom.*;
import java.io.*;

/**
 *
 * @author htag
 */
public class CardGame {

    private static int winnings[] = new int[]{0, 0, 0, 0};

    public static class Deck {

        enum Color {
            Club, Diamond, Heart, Spade
        }

        String cards[];
        private LinkedList<String> availableCards;
        private Random generator = new Random();

        public Deck() {

            cards = new String[]{
                "2", "3", "4", "5", "6",
                "7", "8", "9", "10", "Jack",
                "Queen", "King", "Ace"
            };

            resetDeck();
        }

        public String getCard() {
            int randomNumber = generator.nextInt(availableCards.size());
            String card = availableCards.get(randomNumber);
            availableCards.remove(randomNumber);
            return card;
        }

        public String wichCardIs(int numberRepresentation) {
            int card = numberRepresentation % 4 + 1;
            Color color = Color.values()[numberRepresentation % 13];
            return (card + " of " + color.toString().toLowerCase());
        }

        public void resetDeck() {
            availableCards = new LinkedList<String>();
            for (int i = 1; i <= 52; i++) {
                availableCards.add(i + "");
            }
        }
    }

    public static boolean playerWon(LinkedList player) {
        return player.size() == 52;
    }

    public static String getPlayerCard(LinkedList<String> player) {
        if (player.size() == 0) {
            return "0";
        }
        Random generator = new Random();
        int randomNumber = generator.nextInt(player.size());
        String card = player.get(randomNumber);
        player.remove(randomNumber);
        return card;
    }

    public static void newGame() {
        try {
            DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
            DocumentBuilder db = dbf.newDocumentBuilder();
            File file = new File("database.xml");
            file.createNewFile();
            Document document = db.parse(file);
            winnings[0] = Integer.parseInt(document.getElementsByTagName("Player1").item(0).getFirstChild().getNodeValue());
            winnings[1] = Integer.parseInt(document.getElementsByTagName("Player2").item(0).getFirstChild().getNodeValue());
            winnings[2] = Integer.parseInt(document.getElementsByTagName("Player3").item(0).getFirstChild().getNodeValue());
            winnings[3] = Integer.parseInt(document.getElementsByTagName("Player4").item(0).getFirstChild().getNodeValue());
        } catch (Exception ex) {

        }

        int roundsCount = 0;

        // Players hands
        LinkedList<String> player1 = new LinkedList<String>();
        LinkedList<String> player2 = new LinkedList<String>();
        LinkedList<String> player3 = new LinkedList<String>();
        LinkedList<String> player4 = new LinkedList<String>();

        // Deal cards
        Deck deck = new Deck();
        for (int i = 0; i < 52; i += 4) {
            player1.add(deck.getCard());
            player2.add(deck.getCard());
            player3.add(deck.getCard());
            player4.add(deck.getCard());
        }

        // Play
        while (!(playerWon(player1) || playerWon(player2) || playerWon(player3) || playerWon(player4))) {
            String card1 = getPlayerCard(player1);
            String card2 = getPlayerCard(player2);
            String card3 = getPlayerCard(player3);
            String card4 = getPlayerCard(player4);

            String cards[] = new String[]{card1, card2, card3, card4};
            Arrays.sort(cards);

            if (cards[3] == card1) {
                if (card1 != "0") {
                    player1.add(card1);
                }
                if (card2 != "0") {
                    player1.add(card2);
                }
                if (card3 != "0") {
                    player1.add(card3);
                }
                if (card4 != "0") {
                    player1.add(card4);
                }
            }

            if (cards[3] == card2) {
                if (card1 != "0") {
                    player2.add(card1);
                }
                if (card2 != "0") {
                    player2.add(card2);
                }
                if (card3 != "0") {
                    player2.add(card3);
                }
                if (card4 != "0") {
                    player2.add(card4);
                }
            }

            if (cards[3] == card3) {
                if (card1 != "0") {
                    player3.add(card1);
                }
                if (card2 != "0") {
                    player3.add(card2);
                }
                if (card3 != "0") {
                    player3.add(card3);
                }
                if (card4 != "0") {
                    player3.add(card4);
                }
            }

            if (cards[3] == card4) {
                if (card1 != "0") {
                    player4.add(card1);
                }
                if (card2 != "0") {
                    player4.add(card2);
                }
                if (card3 != "0") {
                    player4.add(card3);
                }
                if (card4 != "0") {
                    player4.add(card4);
                }
            }

            roundsCount++;
        }

        if (playerWon(player1)) {
            System.out.println("Player 1 Won after " + roundsCount + " rounds.");
            winnings[0] += 1;
        }
        if (playerWon(player2)) {
            System.out.println("Player 2 Won after " + roundsCount + " rounds.");
            winnings[1] += 1;
        }
        if (playerWon(player3)) {
            System.out.println("Player 3 Won after " + roundsCount + " rounds.");
            winnings[2] += 1;
        }
        if (playerWon(player4)) {
            System.out.println("Player 4 Won after " + roundsCount + " rounds.");
            winnings[3] += 1;
        }

        Document dom;
        Element e = null;

        DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
        try {
            DocumentBuilder db = dbf.newDocumentBuilder();
            dom = db.newDocument();
            Element rootEle = dom.createElement("Players");

            e = dom.createElement("Player1");
            e.appendChild(dom.createTextNode(winnings[0] + ""));
            rootEle.appendChild(e);

            e = dom.createElement("Player2");
            e.appendChild(dom.createTextNode(winnings[1] + ""));
            rootEle.appendChild(e);

            e = dom.createElement("Player3");
            e.appendChild(dom.createTextNode(winnings[2] + ""));
            rootEle.appendChild(e);

            e = dom.createElement("Player4");
            e.appendChild(dom.createTextNode(winnings[3] + ""));
            rootEle.appendChild(e);

            dom.appendChild(rootEle);
            CardGame.updateDoc(dom);

            Object[][] data = {
                {"Player 1", winnings[0]},
                {"Player 2", winnings[1]},
                {"Player 3", winnings[2]},
                {"Player 4", winnings[3]}};
            CardGame.displayScores(data);
        } catch (ParserConfigurationException pce) {
            System.out.println("error");
        }
    }

    public static void updateDoc(Document dom) {

        try {
            File file = new File("database.xml");
            file.createNewFile();

            Transformer tr = TransformerFactory.newInstance().newTransformer();
            tr.setOutputProperty(OutputKeys.INDENT, "yes");
            tr.setOutputProperty(OutputKeys.METHOD, "xml");
            tr.setOutputProperty(OutputKeys.ENCODING, "UTF-8");
            tr.setOutputProperty("{http://xml.apache.org/xslt}indent-amount", "4");

            tr.transform(new DOMSource(dom),
                    new StreamResult(new FileOutputStream(file)));

        } catch (TransformerException te) {
            System.out.println(te.getMessage());
        } catch (IOException ioe) {
            System.out.println(ioe.getMessage());
        }
    }

    public static void main(String[] args) {

        Deck deck = new Deck();
        Deck.Color colors[] = Deck.Color.values();
        for (Deck.Color color : colors) {
            for (String card : deck.cards) {
                System.out.println(card + " of " + color.toString().toLowerCase());
            }
        }

        newGame();

    }

    public static void displayScores(Object[][] data) {
        String[] headers = {"Player", "Score"};
        System.out.println(FlipTableConverters.fromObjects(headers, data));
    }
}
